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
                "A Hurricane is a powerful tropical weather system characterized by a low-pressure center, organized thunderstorms, and intense sustained winds of at least 74 mph (119 kph).",
            bullets: [
                {
                    text: "Warm Ocean Water",
                    subs: [
                        "Temperatures must be at least 80 farenheit(26.5 celsius) to a depth of about 150 feet to provide the necessary 'fuel' or energy.",
                    ],
                },
                {
                    text: "Moist Air",
                    subs: [
                        "High humidity in the atmosphere allows clouds to form and releases heat as water vapor condenses, which powers the storm's growth.",
                    ],
                },
                {
                    text: "Converging Winds",
                    subs: [
                        "Low-level winds must come together (converge) and push the moist air upward, while low wind shear (little change in wind speed or direction with height) keeps the storm's structure from being torn apart.",
                    ],
                },
            ],
        },
        {
            title: "Landslide",
            description:
                "A landslide is the downward movement of a mass of rock, debris, or earth under the direct influence of gravity. It occurs when the 'driving force' pushing material down a slope becomes stronger than the 'resisting force' (the strength of the soil and rock) holding it in place.",
            bullets: [
                {
                    text: "Saturation by Water",
                    subs: [
                        "Heavy rainfall, rapid snowmelt, or flooding adds weight to the soil and acts as a lubricant, reducing the friction that holds the slope in place.",
                    ],
                },
                {
                    text: "Seismic Activity",
                    subs: [
                        "Earthquakes and volcanic eruptions create powerful vibrations that shake loose soil and rock, causing unstable slopes to collapse.",
                    ],
                },
                {
                    text: "Human Activity",
                    subs: [
                        "Construction, mining, and deforestation (removing roots that anchor the soil) weaken the natural structure of the land and increase the likelihood of a slide.",
                    ],
                },
            ],
        },
        {
            title: "Tsunami",
            description:
                "A tsunami is a series of extremely long ocean waves caused by a large and sudden displacement of the ocean. The name comes from the Japanese words 'tsu' (harbor) and 'nami' (wave).Unlike regular waves caused by wind, tsunamis involve the movement of the entire water column from the seafloor to the surface. ",
            bullets: [
                {
                    text: "Undersea Earthquakes",
                    subs: [
                        "This is the most common cause. When tectonic plates shift abruptly under the ocean floor, they vertically displace a massive amount of water.",
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
                        "Violent underwater explosions or the collapse of a volcanic island into the sea can displace enough water to trigger a tsunami.",
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
