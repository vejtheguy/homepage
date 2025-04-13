<script lang="ts">
	import { PUBLIC_API_KEY } from '$env/static/public';
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';
	import HourTimer from './HourTimer.svelte';

	type WeatherData = {
		location: {
			name: String;
		};
		current: {
			temp_f: Number;
			condition: {
				text: String;
				icon: String;
			};
		};
	};

	let myWeather: WeatherData | null = null;

	const getWeather = async () => {
		const res = await fetch(
			`https://api.weatherapi.com/v1/current.json?key=${PUBLIC_API_KEY}&q=Tucson&aqi=no`
		);

		const data = await res.json();

		myWeather = data;
		console.log(new Date(), data.current.temp_f);
	};

	onMount(() => {
		getWeather();
	});
</script>

<HourTimer on:tick={() => getWeather()} />

{#if myWeather}
	<div class="mr-2 flex flex-col items-end">
		<span class="text-xl"
			>{myWeather.location.name}<img
				src={`https:${myWeather.current.condition.icon}`}
				alt="Weather icon"
				class="inline size-7"
				transition:fade={{ duration: 1500 }}
			/></span
		>
		<span>
			{myWeather.current.condition.text}
			<span>{myWeather.current.temp_f}°F</span>
		</span>
	</div>
{/if}
