<script lang="ts">
    export let date: number;
    export let icon: string;
    export let description: string;
    export let temperature: number;

    const dayOfTheWeek = new Date(date * 1000).toLocaleDateString('en-ZA', {
        weekday: 'long',
    });
</script>

<section class="flex items-center justify-between w-full">
    <p class="w-1/3">{dayOfTheWeek}</p>
    <div class="mr-auto flex items-center">
        <img
            src={`http://openweathermap.org/img/wn/${icon}.png`}
            alt="Daily Weather Icon"
        />
        <small class="capitalize text-slate-600">{description}</small>
    </div>
    <p>{temperature}&deg;</p>
</section>
