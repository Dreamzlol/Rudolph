<script lang="ts">
	type Star = {
		id: number;
		top: string;
		left: string;
		scale: number;
		duration: number;
	};

	const config = {
		count: 100,
		minScale: 0.5,
		maxScale: 1,
		minDuration: 1,
		maxDuration: 3
	} as const;

	const random = (min: number, max: number) => Math.random() * (max - min) + min;

	const stars: Star[] = Array.from({ length: config.count }, (_, i) => ({
		id: i,
		top: `${random(0, 100)}%`,
		left: `${random(0, 100)}%`,
		scale: random(config.minScale, config.maxScale),
		duration: random(config.minDuration, config.maxDuration)
	}));
</script>

<div class="fixed inset-0">
	{#each stars as { id, top, left, scale, duration } (id)}
		<div
			class="animate-twinkle absolute h-1 w-1 rounded-full bg-white"
			style:top
			style:left
			style:transform="scale({scale})"
			style:animation-duration="{duration}s"
		></div>
	{/each}
</div>

<style>
	@keyframes twinkle {
		0%,
		100% {
			opacity: 1;
		}
		50% {
			opacity: 0.1;
		}
	}
	.animate-twinkle {
		animation: twinkle infinite;
	}
</style>
