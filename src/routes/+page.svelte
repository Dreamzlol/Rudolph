<script lang="ts">
	import Headline from '$lib/components/Headline/Headline.svelte';
	import Stars from '$lib/components/Stars/Stars.svelte';
	import Present from '$lib/components/Present/Present.svelte';
	import Snow from '$lib/components/Snow/Snow.svelte';
	import confetti from 'canvas-confetti';

	let isModalOpen = false;

	const toggleModal = () => {
		isModalOpen = !isModalOpen;
		if (isModalOpen) {
			confetti({
				particleCount: 100,
				spread: 70,
				origin: { x: 0.5, y: 0.6 }
			});
			confetti({
				particleCount: 100,
				spread: 70,
				origin: { x: 0.5, y: 0.6 }
			});
		}
	};
</script>

<section
	class="relative flex h-screen flex-col items-center justify-center overflow-hidden bg-[#0D1117]"
>
	<Stars />
	<Snow />

	<div class="pb-32">
		<Headline />
	</div>

	<button class="animate-bounce p-0" on:click={toggleModal}>
		<Present />
	</button>
	<span class="font-bold text-gray-600">Öffne dein Geschenk!</span>

	{#if isModalOpen}
		<div
			class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm"
			on:click={toggleModal}
		>
			<div class="relative w-1/3 rounded-lg bg-white p-8" on:click|stopPropagation>
				<button
					class="absolute right-5 top-3 text-xl text-gray-500 hover:text-black"
					on:click={toggleModal}
				>
					x
				</button>
				<h2 class="mb-4 text-2xl font-bold">Dein Geschenk!</h2>
				<p class="text-gray-700">2x Seagate IronWolf NAS HDD 18TB</p>
				<p class="text-gray-700">1x Socken</p>
				<p class="text-gray-700">1x NewzBay Invite</p>
			</div>
		</div>
	{/if}
</section>
