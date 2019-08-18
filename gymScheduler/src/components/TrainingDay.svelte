<script>

//tableau d'objets de jours
const nbOfDays = [
    { id: 1, text: "One day", value: 1 },
    { id: 2, text: "Two days", value: 2 },
    { id: 3, text: "Three days", value: 3 },
    { id: 4, text: "Four days", value: 4 },
    { id: 5, text: "Five days", value: 5 },
    { id: 6, text: "Six days", value: 6 },
    { id: 7, text: "Seven days", value: 7}
];
//recupération de la selection de l'utilisateur (menu déroulant)
let nbDaysTrainingPerWeek;

</script>

<style></style>

<div>
    <form>
        <select bind:value={nbDaysTrainingPerWeek}>
            <!-- itération sur la collection du tableau d'ojet + association à une clef unique -->
            {#each nbOfDays as day (day.id)} 
                <option value={day}>{day.text}</option>
            {/each}
        </select>
    </form>
    {JSON.stringify(nbDaysTrainingPerWeek)}
</div>