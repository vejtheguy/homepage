<script lang="ts">
	import { createEventDispatcher, onMount } from 'svelte';

	const dispatch = createEventDispatcher();

	onMount(() => {
		const timeLoaded = new Date();
		const timeToHour =
			(59 - timeLoaded.getMinutes()) * 60 * 1000 +
			(60 - timeLoaded.getSeconds()) * 1000 -
			timeLoaded.getMilliseconds();

		const timeout = setTimeout(() => {
			dispatch('tick');

			const interval = setInterval(
				() => {
					dispatch('tick');
				},
				60 * 60 * 1000
			);

			return () => clearInterval(interval);
		}, timeToHour);

		return () => clearTimeout(timeout);
	});
</script>
