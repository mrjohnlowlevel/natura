<script lang="ts">
    const disasters = [
        {
            title: "Earthquake",
            description: `Earthquake is the sudden shaking of the Earth surface caused by the rapid release of energy in the Earth outer layer, called lithospere. This energy creates seismic wave that travel through the ground.`,
            bullets: [
                {
                    text: "Tectonic Plate Shifts (Mantle Convection)",
                    subs: [
                        "Radioactive decay in the Earth's core generates intense heat, warming the semi-fluid asthenosphere.",
                        "This heated material rises in convection cells, spreading horizontally beneath the rigid lithosphere.",
                        "Through basal drag, these currents act like a conveyor belt, moving the plates until they collide or grind past each other",
                        "The accumulated elastic strain energy eventually exceeds the rock's strength, causing a sudden rupture and seismic release.",
                    ],
                },
                {
                    text: "Magmatic Seismicity (Volcanic Activity)",
                    subs: [
                        "As magma intrusion occurs, molten rock forces its way into the crust, fracturing the surrounding country rock.",
                        "The movement of highly pressurized volcanic gases creates harmonic tremors, which are long-duration, low-frequency vibrations.",
                        "A caldera collapse can also trigger major earthquakes when a depleted magma chamber can no longer support the ground above it.",
                    ],
                },
                {
                    text: "Induced Seismicity (Human Activity)",
                    subs: [
                        "Industrial activities like fracking or wastewater injection reduce effective stress by lubricating deep fault lines.",
                        "Reservoir-Induced Seismicity (RIS) occurs when the massive weight of a dam increases pore-pressure in the crust.",
                        "Large-scale crustal unloading from deep mining causes the Earth to rebound, triggering shallow, localized tremors.",
                    ],
                },
            ],
        },
        {
            title: "Hurricane",
            description:
                "Powerful rotating winds Forms over warm oceans Heavy rain and flooding",
            bullets: [
                {
                    text: "Powerful rotating winds",
                    subs: [
                        "Reaches speeds over 74 mph",
                        "Rotates around a calm eye",
                    ],
                },
                {
                    text: "Forms over warm oceans",
                    subs: [
                        "Fueled by warm water moisture",
                        "Common in tropical regions",
                    ],
                },
                {
                    text: "Heavy rain and flooding",
                    subs: [
                        "Causes dangerous storm surges",
                        "Inundates coastal areas",
                    ],
                },
            ],
        },
        {
            title: "Landslide",
            description:
                "Rapid rock/debris flow Triggered by heavy rain Common on steep slopes",
            bullets: [
                {
                    text: "Rapid rock/debris flow",
                    subs: [
                        "Downslope movement of earth material",
                        "Can destroy everything in its path",
                    ],
                },
                {
                    text: "Triggered by external forces",
                    subs: [
                        "Heavy rainfall and storms",
                        "Earthquake vibrations",
                    ],
                },
                {
                    text: "Common on steep slopes",
                    subs: ["High risk in mountainous terrain"],
                },
            ],
        },
        {
            title: "Tsunami",
            description:
                "Large underwater waves Caused by earthquakes High coastal impact",
            bullets: [
                {
                    text: "Large underwater waves",
                    subs: [
                        "Travels at high speeds across oceans",
                        "Grows in height as it nears shore",
                    ],
                },
                {
                    text: "Caused by major disturbances",
                    subs: ["Underwater earthquakes", "Volcanic eruptions"],
                },
                {
                    text: "High coastal impact",
                    subs: ["Washes away low-lying communities"],
                },
            ],
        },
    ];
</script>

<div>
    <div class="mb-60 pl-6 grid grid-cols-1 md:grid-cols-2">
        <div class="sm:text-center">
            <h1 class="font-bold text-4xl font-roboto text-shadow-lg">
                Natura: Natural Disaster Simulator
            </h1>
            <p class="font-thin">
                Learn more about natural disasters and simulate them here, at
                Natura.
            </p>
        </div>
        <div class="md:justify-self-end md:mt-0 mt-6 text-center pr-12">
            <img
                src="/natura/icon.jpeg"
                alt="Natura"
                height="200px"
                width="200px"
                class="rounded-2xl shadow-md hover:scale-105 transition-transform duration-200"
            />
        </div>
    </div>
    <div id="learn-more" class="p-6 bg-white">
        <h1
            class="font-bold text-4xl font-roboto text-center text-shadow-lg mb-2"
        >
            Natural Disasters
        </h1>
        <div
            class="text-center grid grid-cols-1 md:grid-cols-2 justify-items-center bg-[#edf2fb] p-12 gap-2.5 rounded-sm"
        >
            {#each disasters as disaster}
                <div
                    class="bg-white size-fit grid grid-cols-1 items-center justify-center shadow-sm rounded-2xl p-6"
                >
                    <h1 class="mb-5 bold text-2xl">{disaster.title}</h1>

                    <p class="mb-5 px-6 text-center">
                        {@html disaster.description}
                    </p>

                    <!-- Clean, aligned bullet point layout structure -->
                    <ul class="list-disc pl-8 text-left space-y-2 w-full">
                        {#each disaster.bullets as bullet}
                            <li class="font-semibold text-gray-800">
                                {bullet.text}
                            </li>

                            {#if bullet.subs && bullet.subs.length > 0}
                                <!-- Indented sub-bullets list -->
                                <ul
                                    class="list-circle pl-6 mt-1 space-y-1 text-gray-600 font-normal text-sm"
                                >
                                    {#each bullet.subs as subPoint}
                                        <li>{subPoint}</li>
                                    {/each}
                                </ul>
                            {/if}
                        {/each}
                    </ul>
                </div>
            {/each}
        </div>
    </div>
</div>
