<script>
	import Clock from '$lib/components/Clock.svelte';
	import Background from '$lib/components/Background.svelte';
	import Weather from '$lib/components/Weather.svelte';
</script>

<div class="relative">
	<Background />
	<div
		class="font-poppins fixed top-0 right-0 flex min-h-screen flex-col items-end justify-between p-12 font-light tracking-wider text-white text-shadow-lg"
	>
		<Clock />
		<Weather />
	</div>
</div>
