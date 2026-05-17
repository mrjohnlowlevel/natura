<script lang="ts">
    import { onMount } from "svelte";

    let canvas: HTMLCanvasElement;
    let ctx: CanvasRenderingContext2D | null = null;
    let isTsunamiActive = false;
    let activeTool = "none"; // 'tsunami' or 'none'

    // Game state arrays
    let buildings: Array<{
        x: number;
        y: number;
        width: number;
        height: number;
        health: number;
        color: string;
    }> = [];
    let waterParticles: Array<{
        x: number;
        y: number;
        vx: number;
        vy: number;
        size: number;
    }> = [];

    const CANVAS_WIDTH = 800;
    const CANVAS_HEIGHT = 400;
    const GROUND_Y = 350;

    // Initialize the city grid with simple buildings
    function initCity() {
        buildings = [];
        waterParticles = [];
        isTsunamiActive = false;

        const buildingWidth = 50;
        const gap = 25;
        const colors = ["#64748b", "#475569", "#334155", "#1e293b"]; // Varied slate grays

        // Row of 9 buildings across the screen
        for (let i = 0; i < 9; i++) {
            const height = 100 + Math.random() * 120; // Random heights
            buildings.push({
                x: 100 + i * (buildingWidth + gap),
                y: GROUND_Y - height,
                width: buildingWidth,
                height: height,
                health: 100,
                color: colors[i % colors.length],
            });
        }
    }

    // Trigger the disaster loop
    function triggerTsunami() {
        if (isTsunamiActive) return;
        isTsunamiActive = true;

        // Spawn a massive wall of water particles just off-screen left
        for (let i = 0; i < 150; i++) {
            waterParticles.push({
                x: -Math.random() * 100,
                y: GROUND_Y - Math.random() * 180, // High wave height
                vx: 4 + Math.random() * 3, // Moving fast right
                vy: (Math.random() - 0.5) * 2,
                size: 15 + Math.random() * 15,
            });
        }
    }

    // Handle canvas clicks to manually damage buildings (City Smash style)
    function handleCanvasClick(event: MouseEvent) {
        const rect = canvas.getBoundingClientRect();
        const clickX = event.clientX - rect.left;
        const clickY = event.clientY - rect.top;

        // If tsunami tool is armed, click anywhere to unleash it
        if (activeTool === "tsunami") {
            triggerTsunami();
            activeTool = "none";
            return;
        }

        // Otherwise, click specifically on buildings to smash them manually
        buildings.forEach((b) => {
            if (
                clickX >= b.x &&
                clickX <= b.x + b.width &&
                clickY >= b.y &&
                clickY <= b.y + b.height
            ) {
                b.health -= 35; // Damage building
                if (b.health < 0) b.health = 0;
            }
        });
    }

    // The central game loop
    function updateAndRender() {
        if (!ctx) return;
        const c = ctx;

        // 1. Clear Screen
        c.fillStyle = "#f0f4f8"; // Sky blue tint
        c.fillRect(0, 0, CANVAS_WIDTH, CANVAS_HEIGHT);

        // 2. Draw Environment Ground
        c.fillStyle = "#a1a1aa"; // Concrete gray ground
        c.fillRect(0, GROUND_Y, CANVAS_WIDTH, CANVAS_HEIGHT - GROUND_Y);

        // 3. Update & Draw Buildings
        buildings.forEach((b) => {
            if (b.health > 0) {
                // Calculate dynamic height based on structural health
                const currentHeight = b.height * (b.health / 100);
                const currentY = GROUND_Y - currentHeight;

                c.fillStyle = b.color;
                c.fillRect(b.x, currentY, b.width, currentHeight);

                // Draw simple window lines to make them look like skyscrapers
                c.fillStyle = b.health < 40 ? "#451a03" : "#fef08a"; // Windows go dark if broken
                for (let wy = currentY + 10; wy < GROUND_Y - 10; wy += 25) {
                    c.fillRect(b.x + 10, wy, 10, 8);
                    c.fillRect(b.x + 30, wy, 10, 8);
                }
            } else {
                // Ruined rubble base
                c.fillStyle = "#4b5563";
                c.fillRect(b.x, GROUND_Y - 15, b.width, 15);
            }
        });

        // 4. Update & Draw Water Physics
        waterParticles.forEach((p, index) => {
            p.x += p.vx;
            p.y += p.vy;
            p.vy += 0.1; // Artificial gravity to pull splashing water down

            // Keep water sliding across the concrete floor
            if (p.y > GROUND_Y - p.size / 2) {
                p.y = GROUND_Y - p.size / 2;
                p.vy = -p.vy * 0.2; // Bounce slightly off floor
            }

            // Check collision between water and buildings
            buildings.forEach((b) => {
                if (b.health > 0) {
                    const currentHeight = b.height * (b.health / 100);
                    const currentY = GROUND_Y - currentHeight;

                    // Simple Box-vs-Circle physics check
                    if (
                        p.x + p.size / 2 >= b.x &&
                        p.x - p.size / 2 <= b.x + b.width &&
                        p.y >= currentY
                    ) {
                        b.health -= 0.6; // Erosion damage over time as wave hits
                        p.vx *= 0.85; // Water loses velocity when hitting structures
                        p.vy -= 1.5; // Splash upwards!
                    }
                }
            });

            // Render the water blob
            c.fillStyle = "rgba(14, 116, 144, 0.65)"; // Transparent Cyan-Blue
            c.beginPath();
            c.arc(p.x, p.y, p.size, 0, Math.PI * 2);
            c.fill();

            // Clean up particles that leave the screen to save memory
            if (p.x > CANVAS_WIDTH + 50) {
                waterParticles.splice(index, 1);
            }
        });

        // Request next animation frame (60 FPS loop)
        requestAnimationFrame(updateAndRender);
    }

    onMount(() => {
        ctx = canvas.getContext("2d");
        initCity();
        updateAndRender();
    });
</script>

<div id="sim" class="max-w-4xl mx-auto my-8 p-6 bg-white rounded-sm shadow-md font-sans">
    <!-- Canvas Viewport Layout -->
    <div
        class="relative border-4 border-slate-700 rounded-lg overflow-hidden bg-slate-100 flex justify-center"
    >
        <canvas
            bind:this={canvas}
            width={CANVAS_WIDTH}
            height={CANVAS_HEIGHT}
            on:click={handleCanvasClick}
            class="cursor-crosshair block"
        ></canvas>

        {#if activeTool !== "none"}
            <div
                class="absolute top-4 left-4 bg-red-600 text-white text-xs uppercase px-3 py-1.5 rounded-full font-bold animate-pulse tracking-wide shadow-md"
            >
                Click on screen to drop Tsunami
            </div>
        {/if}
    </div>

    <!-- Dashboard/Control Panel Panel Options -->
    <div class="mt-6 p-6 bg-[#edf2fb] rounded-sm border border-slate-200">
        <h3
            class="text-sm font-bold uppercase tracking-wider text-slate-700 mb-4"
        >
            Disaster Control Interface
        </h3>

        <div class="flex flex-wrap gap-4 items-center justify-between">
            <!-- Primary Disaster Trigger Trigger -->
            <div class="flex gap-3">
                <button
                    on:click={() => (activeTool = "tsunami")}
                    class="px-6 py-3 font-semibold text-white rounded-md shadow-sm transition-all duration-150 transform active:scale-95
            {activeTool === 'tsunami'
                        ? 'bg-red-500 ring-4 ring-red-300'
                        : 'bg-cyan-700 hover:bg-cyan-600'}"
                >
                    🌊 Arm Tsunami
                </button>

                <button
                    on:click={triggerTsunami}
                    class="px-5 py-3 bg-slate-800 text-slate-200 font-medium rounded-md hover:bg-slate-700 transition-colors shadow-sm"
                >
                    Instant Launch
                </button>
            </div>

            <!-- Reset Utility Tool -->
            <button
                on:click={initCity}
                class="px-5 py-3 border-2 border-slate-300 text-slate-700 font-medium rounded-md hover:bg-white transition-colors bg-transparent"
            >
                Rebuild City 🏢
            </button>
        </div>

        <!-- Quick Tip Text Helper -->
        <p class="mt-4 text-xs text-slate-500 italic">
            💡: You can also click directly on the skyscraper glass
            windows anytime to smash them manually with seismic force!
        </p>
    </div>
</div>
