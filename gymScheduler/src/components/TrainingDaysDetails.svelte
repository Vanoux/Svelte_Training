<script>
    export let title;
    let exercise = {
        activity: "",
        series: 4,
        repetitions: 10
    }

    let exercises = [];

    function handleSubmit() {
        exercises = [...exercises, { ...exercise}]; 
        //Ajoute dans la variable exercises un clone de l'objet exercise à la soumission du form
        console.log('exercises', exercises)
    }

</script>

<style></style>

<!-- Détails des exercices -->
<div>
    <h2>{title}</h2>
    <div>
        <form on:submit|preventDefault={handleSubmit}>
            <div>
                <label for="activity">Activity</label>
                <input type="text" id="activity" bind:value={exercise.activity}>
            </div>
            <div>
                <label for="series">Series</label>
                <input type="number" id="series" bind:value={exercise.series}>
            </div>
            <div>
                <label for="repetitions">Repetitions</label>
                <input type="number" id="repetitions" bind:value={exercise.repetitions}>
            </div>
            <button type="submit">Add exercise</button>
        </form>
    </div>   
</div>

<!-- Liste les exercices en parcourant le tableau exercises -->
<div>
    <ul>
    {#each exercises as exo}
        <li>{exo.activity} : {exo.series} series of {exo.repetitions}</li>
    {/each}
    </ul>
</div>