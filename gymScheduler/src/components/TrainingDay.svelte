<script>
import TrainingDaysDetails from "./TrainingDaysDetails.svelte";
import TrainingWeekSummary from "./TrainingWeekSummary.svelte";


//tableau d'objets de jours
const nbOfDays = [
    { id: 1, text: "One day", value: [1] },
    { id: 2, text: "Two days", value: [1, 2] },
    { id: 3, text: "Three days", value: [1, 2, 3] },
    { id: 4, text: "Four days", value: [1, 2, 3, 4] },
    { id: 5, text: "Five days", value: [1, 2, 3, 4, 5] },
    { id: 6, text: "Six days", value: [1, 2, 3, 4, 5, 6] },
    { id: 7, text: "Seven days", value: [1, 2, 3, 4, 5, 6, 7]}
];
//recupération de la selection de l'utilisateur (menu déroulant)
let nbDaysTrainingPerWeek;
let isSummaryReady = false;
//résumé des entrainements
let summary = [];

function handleNewExercise(event) {
    console.log("on:add-exercise", event.detail);
    summary = [...summary, event.detail];
    isSummaryReady = false;
}

function generateSummary() {
    isSummaryReady = true;
}

</script>

<style>
    .all-days {
            border: 5px solid chocolate;
            margin: 10px;
        }

    .training-day-details {
        border: 2px solid chartreuse;
        margin: 10px;
        padding: 5px;
    }
</style>

<!-- Dropdown list -->
<div>
    <form>
        <select bind:value={nbDaysTrainingPerWeek}>
            <!-- itération sur la collection du tableau d'ojet + association à une clef unique (day.id)-->
            {#each nbOfDays as day (day.id)} 
                <option value={day}>{day.text} per week</option>
            {/each}
        </select>
    </form>
    {JSON.stringify(nbDaysTrainingPerWeek)}
</div>

{#if nbDaysTrainingPerWeek}
<!-- Affichage du nb de jours d'entrainement du Component TrainingDaysDetails-->
    <div class="all-days">
        {#each nbDaysTrainingPerWeek.value as dayNumber, index}
        <div class="training-day-details">
            <TrainingDaysDetails title={`Day ${++index}`} on:add-exercise={handleNewExercise}></TrainingDaysDetails>
        </div>
        {/each}
    </div>
    {#if isSummaryReady}
    <!-- Passage de 2 props (summary & days) dans le component TrainingWeekSummary -->
    <TrainingWeekSummary summary={summary} days={nbDaysTrainingPerWeek.value.length}></TrainingWeekSummary>
    {/if}
    <button on:click={generateSummary}>Generate summary</button>
{/if}

