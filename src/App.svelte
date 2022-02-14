<script>
	import TimerModule from './TimerModule.svelte';

	let work_duration
</script>

<div class="page">
<h1>
	_worky
	<img class="logo" src="/favicon.png"/>
</h1>

<main>
	<TimerModule name="_work" duration={25} />
	<TimerModule name="_break" duration={5} />
</main>

<a href="https://music.youtube.com/watch?v=VfiQTUL3Ld8&list=RDAMVMVfiQTUL3Ld8">
	Look That Way - Sports Day
</a>
</div>

<style>
	main {
		display:flex;
		min-height:80vh;
		align-items:center;
		justify-content:space-evenly;
		width : 80%;
	}

	.page {
		display:flex;
		flex-direction: column;
		align-items:center;
		justify-content:space-around;
		min-height:100vh;
	}

	.logo {
		height:1.2rem;
	}

	@media only screen and (max-width: 600px) {
	main {
		flex-direction: column;
	}
	}

</style>
