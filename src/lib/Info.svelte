<script lang="ts">
    const disasters = [
        {
            title: "Earthquake",
            description: `An <span style="font-weight: bold;">Earthquake</span> is the sudden shaking of the Earth surface caused by the rapid release of energy in the Earth outer layer, called lithosphere. This energy creates <span style="font-weight: bold;">seismic waves</span> that travel through the ground.`,
            bullets: [
                {
                    text: "Tectonic Plate Shifts (Mantle Convection)",
                    subs: [
                        "<span style='font-weight: bold;'>Convection currents</span> move tectonic plates, building up intense <span style='font-weight: bold;'>strain energy</span> until the rock ruptures along <span style='font-weight: bold;'>fault lines</span>.",
                    ],
                },
                {
                    text: "Magmatic Seismicity (Volcanic Activity)",
                    subs: [
                        "<span style='font-weight: bold;'>Rising magma</span> forces its way into the crust, fracturing surrounding rock and creating vibrations known as <span style='font-weight: bold;'>harmonic tremors</span>.",
                    ],
                },
                {
                    text: "Induced Seismicity (Human Activity)",
                    subs: [
                        "Human operations like <span style='font-weight: bold;'>fracking</span>, <span style='font-weight: bold;'>deep mining</span>, or building <span style='font-weight: bold;'>dam reservoirs</span> alter ground pressure and trigger shallow tremors.",
                    ],
                },
            ],
        },
        {
            title: "Hurricane",
            description: `A <span style="font-weight: bold;">Hurricane</span> is a powerful tropical weather system characterized by a <span style="font-weight: bold;">low-pressure center</span>, organized thunderstorms, and intense sustained winds of at least 74 mph (119 kph).`,
            bullets: [
                {
                    text: "Warm Ocean Water",
                    subs: [
                        "Temperatures must be at least <span style='font-weight: bold;'>80 Fahrenheit (26.5 Celsius)</span> to a depth of about 150 feet to provide the necessary <span style='font-weight: bold;'>fuel or energy</span>.",
                    ],
                },
                {
                    text: "Moist Air",
                    subs: [
                        "<span style='font-weight: bold;'>High humidity</span> in the atmosphere allows clouds to form and releases heat as <span style='font-weight: bold;'>water vapor condenses</span>, which powers the storm's growth.",
                    ],
                },
                {
                    text: "Converging Winds",
                    subs: [
                        "Low-level winds must come together (<span style='font-weight: bold;'>converge</span>) and push the moist air upward, while <span style='font-weight: bold;'>low wind shear</span> keeps the storm's structure from being torn apart.",
                    ],
                },
            ],
        },
        {
            title: "Landslide",
            description: `A <span style="font-weight: bold;">landslide</span> is the downward movement of a mass of rock, debris, or earth under the direct influence of <span style="font-weight: bold;">gravity</span>. It occurs when the driving force pushing material down a slope becomes stronger than the resisting force holding it in place.`,
            bullets: [
                {
                    text: "Saturation by Water",
                    subs: [
                        "<span style='font-weight: bold;'>Heavy rainfall</span>, rapid snowmelt, or flooding adds weight to the soil and acts as a <span style='font-weight: bold;'>lubricant</span>, reducing the friction that holds the slope in place.",
                    ],
                },
                {
                    text: "Seismic Activity",
                    subs: [
                        "<span style='font-weight: bold;'>Earthquakes</span> and volcanic eruptions create powerful vibrations that shake loose soil and rock, causing <span style='font-weight: bold;'>unstable slopes to collapse</span>.",
                    ],
                },
                {
                    text: "Human Activity",
                    subs: [
                        "Construction, mining, and <span style='font-weight: bold;'>deforestation</span> (removing roots that anchor the soil) weaken the natural structure of the land and increase the likelihood of a slide.",
                    ],
                },
            ],
        },
        {
            title: "Tsunami",
            description: `A <span style="font-weight: bold;">tsunami</span> is a series of extremely long ocean waves caused by a large and sudden <span style="font-weight: bold;">displacement of the ocean</span>. Unlike regular waves caused by wind, tsunamis involve the movement of the entire water column from the seafloor to the surface.`,
            bullets: [
                {
                    text: "Undersea Earthquakes",
                    subs: [
                        "This is the most common cause. When tectonic plates shift abruptly under the ocean floor, they vertically displace a massive amount of <span style='font-weight: bold;'>water column</span>.",
                    ],
                },
                {
                    text: "Underwater Landslides",
                    subs: [
                        "Large masses of rock and sediment sliding down steep slopes on the seafloor (often triggered by an earthquake) push water out of the way, creating powerful waves.",
                    ],
                },
                {
                    text: "Volcanic Eruptions",
                    subs: [
                        "Violent <span style='font-weight: bold;'>underwater explosions</span> or the collapse of a volcanic island into the sea can displace enough water to trigger a tsunami.",
                    ],
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
            class="text-center grid grid-cols-1 justify-items-center bg-[#edf2fb] p-12 gap-2.5 rounded-sm"
        >
            {#each disasters as disaster}
                <div
                    class="bg-white size-fit grid grid-cols-1 items-center justify-center shadow-sm rounded-2xl p-6"
                >
                    <h1 class="mb-5 font-bold text-2xl">{disaster.title}</h1>

                    <p class="mb-5 px-6 text-center">
                        {disaster.description}
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
