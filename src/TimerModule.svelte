<script>
	import Timer from './Timer.svelte';
	import DurationInput from './DurationInput.svelte';
	import {onMount} from 'svelte';

	export let duration;
	export let name = "Work";

	let triedLoading = false;

	onMount(() => {
		let storedLocation = localStorage.getItem(`duration_${name}`);

		if(storedLocation !== null) duration = Number.parseFloat(storedLocation);

		triedLoading = true;
	});

	$: if (triedLoading) {
		localStorage.setItem(`duration_${name}`,duration);
	}

	let running;
</script>


<main>
	<h1> {name} </h1>

	<Timer bind:running={running} duration={duration} />	

		
	{#if !running}

	<DurationInput bind:value={duration} />	

	{/if}
</main>

<style>
	main {
		display:flex;
		flex-direction:column;
		align-items:center;
		justify-content:space-evenly;

		width: calc(min(50vw,10cm));
		height: calc(min(30vh,10cm));
		background: #815E5B;
		border: #BAD1CD 2px solid;
	}
</style>
