<script>
	export let value = 25;
</script>

<svelte:options accessors/>

<div>
	<input type="text" bind:value = {value}/> 
	<button class="no-border" on:click={() => value--}>
		-
	</button>

	<button class="no-border" on:click={() => value++}>
		+
	</button>
	<span> mins <span>
</div>

<style>
	div {
		font-size:2rem;
		display:flex;
		justify-content:flex-end;
		align-items:center;
	}

	div * {
		margin-right: 10px;
	}
</style>
