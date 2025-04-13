<script>
	import { fade } from 'svelte/transition';
	import HourTimer from './HourTimer.svelte';

	const randomNum = () => {
		return Math.floor(Math.random() * 6) + 1;
	};

	let num = randomNum();
</script>

<HourTimer on:tick={() => (num = randomNum())} />

{#key num}
	<div
		style="background-image: url('src/lib/imgs/img{num}.jpg')"
		transition:fade={{ duration: 1500 }}
		class="absolute z-[-1] min-h-screen w-full bg-cover bg-center bg-no-repeat"
	></div>
{/key}
