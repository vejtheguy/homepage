<script lang="ts">
	import { fade } from 'svelte/transition';
	import HourTimer from './HourTimer.svelte';
	import { onMount } from 'svelte';

	let num: number;
	let hasMounted = false;

	const getNum = () => {
		let newNum = randomNum();

		while (newNum === num) {
			newNum = randomNum();
		}

		return newNum;
	};

	const randomNum = () => {
		return Math.floor(Math.random() * 6) + 1;
	};

	onMount(() => {
		num = getNum();
		hasMounted = true;
	});
</script>

<HourTimer on:tick={() => (num = getNum())} />

{#if hasMounted}
	{#key num}
		<div
			style="background-image: url('/imgs/img{num}.jpg')"
			transition:fade={{ duration: 1500 }}
			class="absolute z-[-1] min-h-screen w-full bg-cover bg-center bg-no-repeat"
		></div>
	{/key}
{/if}
