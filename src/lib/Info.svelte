<script lang="ts">
    const disasters = [
        {
            title: "Earthquake",
            description: "Earthquake is the sudden shaking of the Earth surface caused by the rapid release of energy in the Earth outer layer, called lithospere. This energy creates seismic waves that travel through the ground.",
            bullets: ["Sudden ground shaking", "Tectonic plate shifts", "Measured by seismographs"],
        },
        {
            title: "Hurricane",
            description: "Powerful rotating winds Forms over warm oceans Heavy rain and flooding",
            bullets: ["Powerful rotating winds", "Forms over warm oceans", "Heavy rain and flooding"],
        },
        {
            title: "Landslide",
            description: "Rapid rock/debris flow Triggered by heavy rain Common on steep slopes",
            bullets: ["Rapid rock/debris flow", "Triggered by heavy rain", "Common on steep slopes"]
        },
        {
            title: "Tsunami",
            description: "Large underwater waves Caused by earthquakes High coastal impact",
            bullets: ["Large underwater waves", "Caused by earthquakes", "High coastal impact"],
        }
    ]
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
        <div class="text-center grid grid-cols-1 md:grid-cols-2 justify-items-center bg-[#edf2fb] p-12 gap-2.5 rounded-sm">
            {#each disasters as disaster }
                <div class="bg-white size-fit grid grid-cols-1 items-center justify-center shadow-sm rounded-2xl">
                    <h1 class="mb-5 bold text-2xl">{ disaster.title }</h1>
                    <p class="mb-5 p-6">{ disaster.description }</p>
                    <ul>
                        {#each disaster.bullets as point}
                            <li>・ { point }</li>
                        {/each}
                    </ul>
                </div>
            {/each}
        </div>
    </div>
</div>
