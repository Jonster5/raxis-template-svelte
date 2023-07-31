<script lang="ts">
	import { onMount } from 'svelte';
	import { ECS } from 'raxis';
	import { CanvasSettings, KeysToTrack, defaultPlugins } from 'raxis-plugins';

	let target: HTMLElement;

	const ecs = new ECS().insertPlugins(...defaultPlugins);

	onMount(() => {
		ecs.insertResource(
			new CanvasSettings({
				target,
				width: 2000,
			})
		)
			.insertResource(new KeysToTrack([]))
			.run();
	});
</script>

<main>
	<div bind:this={target} />
</main>

<style lang="scss">
	main {
		width: 100%;
		height: 100%;

		div {
			width: 60%;
			height: 60%;
		}
	}
</style>
