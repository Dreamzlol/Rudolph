<script lang="ts">
	type Snowflake = {
		id: number;
		left: string;
		opacity: number;
		size: string;
		duration: number;
	};

	const config = {
		count: 100,
		minDuration: 6,
		maxDuration: 11,
		minSize: 10,
		maxSize: 20
	} as const;

	const random = (min: number, max: number) => Math.random() * (max - min) + min;

	const snowflakes: Snowflake[] = Array.from({ length: config.count }, (_, i) => ({
		id: i,
		left: `${random(0, 100)}%`,
		opacity: random(0, 1),
		size: `${random(config.minSize, config.maxSize)}px`,
		duration: random(config.minDuration, config.maxDuration)
	}));
</script>

<div class="pointer-events-none fixed inset-0 z-50">
	{#each snowflakes as { id, left, opacity, size, duration } (id)}
		<div
			class="snowflake fixed text-white"
			style:left
			style:opacity
			style:font-size={size}
			style:animation-duration="{duration}s"
		>
			❅
		</div>
	{/each}
</div>

<style>
	.snowflake {
		animation: fall linear infinite;
	}

	@keyframes fall {
		from {
			transform: translateY(-10vh);
		}
		to {
			transform: translateY(100vh);
		}
	}
</style>
