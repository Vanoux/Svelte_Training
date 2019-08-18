<!-- COMPOSANT TEXTAREA + BUTTON SEND -->
<script>
	import { createEventDispatcher } from 'svelte'; //Importe eventDispatcher pour des custom event de l'enfant au parent

	const dispatch = createEventDispatcher(); //Appelle l'eventDispatcher importé

    let message = "";
	let author = ""; 
	let maxLength = 24;
	$: nbCaracters = message.length; //$: permet de dire en svelte que l'on veut utiliser cette variable(pas besoin de lui mettre var ou let) pour la recalculer = il va surveiller ce qui est à droite du signe égal 
	$: disabled = message.length > maxLength ? true : false;
    
    function saveMessage() {
		const newMessage = {
			id: Date.now(),
			text: message,
			author: author || 'anonymous',
			date: new Date
		};
		dispatch('message', newMessage) //custom event
		message = ""; //pour vider le textarea une fois le message envoyé
		author = ""; //pour vider l'input de l'author une fois le message envoyé
	};
</script>

<style>
	.nameText {
		width: 576.80px;
	}
	button:disabled {
		color: gray;
	}
	.alert {
		color: orangered;
	}
</style>


<input class="nameText" type="text" title="Enter your Name" placeholder="Name" bind:value={author}>
<br>
<textarea title="Enter your message" placeholder="Message" cols="50" rows="5" bind:value={message}></textarea> 
<!--Plus besoin d'écouter l'input event avec on:input => Grâce à bind:value, on lie directement la variable que l'on veut binder (peut marcher dans les 2 sens (2waybind)--> 
<br>
<button on:click={saveMessage} disabled={disabled}>Send</button> <!-- En appuyant sur send, on envoie un customEvent qui s'appelle message-->
<span class:alert={nbCaracters > maxLength}>{nbCaracters}</span> <!-- Pour appliquer une classe conditionnellement = class:ClassQueLonVeutAfficherConditionnellement = Condition -->
{#if disabled}
	<span class="alert">(Message too long !)</span>
{/if}


