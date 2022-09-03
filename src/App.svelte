<script lang="ts">
    import DailySummary from './DailySummary.svelte';

    // Grab lat and long from https://www.google.com/maps
    const lat: string = '-26.0592554';
    const long: string = '27.9875983';

    // Get a key from https://openweathermap.org/api/one-call-3
    const apiKey: string = 'xxxxxxxxxxxxxxxx';

    const data = fetch(
        `https://api.openweathermap.org/data/3.0/onecall?lat=${lat}&lon=${long}&appid=${apiKey}&exclude=hourly&units=metric`
    )
        .then((response) => response.json())
        .catch((error) => console.error(error));
</script>

<main
    class="flex flex-col justify-center items-center text-white max-w-screen-sm mx-auto"
>
    {#await data then { current, daily }}
        <h1 class="text-4xl">Svelte Weather App</h1>
        <img
            class="h-[100px] w-[100px]"
            src={`http://openweathermap.org/img/wn/${current.weather[0].icon}@2x.png`}
            alt="Weather Icon"
        />
        <small class="capitalize text-slate-600 mb-4 -mt-4"
            >{current.weather[0].description}</small
        >
        <p class="text-5xl">{current.temp}&deg;</p>
        <hr class="border-1 border-slate-600 w-full my-8" />
        {#each daily as day}
            <DailySummary
                date={day.dt}
                icon={day.weather[0].icon}
                description={day.weather[0].description}
                temperature={day.temp.day}
            />
        {/each}
    {/await}
</main>
