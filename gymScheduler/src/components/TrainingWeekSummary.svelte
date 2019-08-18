<script>
//life cycle hook pour ne pas executer trop tôt du code
    import { onMount } from 'svelte';
//Rend accessible les propriétés de ces 2 variables props de App.svelte
    export let summary;
    export let days;
    let formattedData;
    let isDataFormatted = false;

    function prepareSummary() {
        //accumulator ressemble à {"day 1": [{}, {}], "day 2": [{}, {}]}
        //current ressemble à {activity: 'squat', series: 4, repetitions: 10, title: 'Day 1'}
        formattedData = summary.reduce((accumulator, current) => {
            if (Object.keys(accumulator).includes(current.title)) {
                accumulator[current.title] = [...accumulator[current.title], current]
            } else {
                accumulator[current.title] = [current];
            }
            return accumulator;
        }, {});
        isDataFormatted = true;
        console.log(formattedData);
    }
    onMount(() => { //life cycle hook callback
        console.log('onMount');
        prepareSummary();
    })   
</script>

<style></style>

{#if isDataFormatted}
    <h2>Summary</h2>
    {#if summary.length}
        {#each Object.keys(formattedData) as day}
        <h2>{day}</h2>
            {#each formattedData[day] as exo}
                {exo.activity} : {exo.series} series of {exo.repetitions} repetitions<br>
            {/each}
        {/each}
    {:else}
        <div>Missing data ! Please add exercises !</div>
    {/if}
{/if}