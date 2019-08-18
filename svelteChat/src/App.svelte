<!-- Script Js Svelte -->
<script>
import MessageCreate from './MessageCreate.svelte';
	export let name; //préfix export pour la variable soit accessible depuis l'extérieur
	let messages = [];
	let isVisible = true;

	function addMessage(event) { //fonction qui met à disposition un event custom
		console.log(event); //on trouve une propriété detail avec les informations de l'objet message
		messages = [event.detail, ...messages]; //récupération de ses informations au message pré-existant (avec la syntaxe ...messages)
	};

	const optionsDate = { //formatage date
		weekday: "short",
		year: "numeric",
		month: "long",
		day: "numeric",
		hour12: false,
		hour: "numeric",
		minute: "2-digit",
		second: "2-digit"
	};
	const formatter = new Intl.DateTimeFormat("fr-FR", optionsDate)

	function toggle() {
		isVisible = !isVisible;
	};
</script>

<!-- Style CSS Svelte -->
<style>
	h1 {
		color: purple;
	}
	.author {
		font-weight: bold;
	}
</style>

<!-- Html Svelte -->
<h1>{name}</h1>

<!-- Bouton pour cacher ou montrer le component Message (input+textArea+btn send) -->
<button on:click={toggle}>{isVisible ? 'Hide' : 'Show'}</button>
<br>
{#if isVisible}
	<!-- props pour passer des éléments du component parent à l'enfant (variable dans l'élement component enfant, ex: <Message author="Bob"/> ) et event (avec on:) pour l'inverse -->
	<MessageCreate on:message={addMessage} /> <!-- on écoute l'event on:message qui appelle la fonction addMessage--> 
{/if}

<div>
	<h2>Messages</h2>
	<!-- Itération de l'array d'objets {messages}  -->
	{#each messages as content}
		<div class="author">By {content.author} on {formatter.format(content.date)}</div>
		<div>{content.text}</div>
		<hr>
	{/each}
</div>
