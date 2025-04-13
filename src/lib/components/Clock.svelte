<script>
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';

	let date = new Date();
	$: hour = date.getHours() % 12 || 12;
	$: min = date.getMinutes().toString().padStart(2, '0');
	$: month = date.toLocaleString('default', { month: 'long' });
	$: day = date.getDate();
	$: weekday = date.toLocaleString('default', { weekday: 'long' });

	onMount(() => {
		const interval = setInterval(() => {
			date = new Date();
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>

<div class="flex flex-col items-end">
	<span class="text-9xl" transition:fade={{ duration: 1500 }}>{hour}:{min}</span>
	<span class="mr-2 text-xl">{weekday}, {month} {day}</span>
</div>
