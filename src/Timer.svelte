<script>
	export let duration = 0;
	export let additional_duration = 0;

	let secs_duration;

	export let running = false;

	$: secs_duration = duration * 60 + additional_duration * 60;

	let timer_string = 	"00:00";

	let start_time;

	function toggle() {
		if(!running) {
			running = true;
			start_time = Math.floor(Date.now() / 1000);
		} else {
			running = false;
			additional_duration = 0;
			setSound(false);
		}
	}

	function pad0(n) {
		if(n < 10) {
			return "0" + n;
		}
		return "" + n;
	}

	function addTime(n) {
		additional_duration += n;
	}

	let playing = false;
	let audioSource;

	function setSound(f) {
		if(f) {
			if(!playing) {
				audioSource.currentTime = 0;
				audioSource.play();
				playing = true;
			}
		} else {
			if(playing) {
				audioSource.pause();
				playing = false;
			}
		}
	}

	function update() {
		if(!running) {
			timer_string = pad0(Math.floor(secs_duration / 60)) + ":" + pad0((Math.floor(secs_duration) % 60));
		} else {
			let current_time = secs_duration - (Math.floor(Date.now() / 1000) - start_time);

			if(current_time <= 0) {
				setSound(true);
			} else {
				setSound(false);
			}

			timer_string = pad0(Math.trunc(current_time / 60)) + ":" + pad0((Math.floor(Math.abs(current_time)) % 60));
		}

		window.requestAnimationFrame(update);
	}

	update();
</script>

<audio bind:this={audioSource} loop>
	<source src="/look_that_way.opus" type="audio/ogg">
</audio>



<h1 class:running={running} class:overrunning={playing}>
	{timer_string}
</h1>

<button on:click={toggle}>
	{running ? "stop" : "start"}
</button>

{#if running}
<button class="no-border" on:click={() => addTime(1)}>
	+1 min
</button>
{/if}

<style>
	h1 {
		transition: font-size 0.5s ease;
	}

	h1.running {
		font-size: 250%;
	}

	h1.overrunning {
		color: #E086D3;
	}
</style>


