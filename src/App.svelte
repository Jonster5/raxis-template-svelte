<script lang="ts">
	import { onMount } from 'svelte';
	import { ECS, Vec2 } from 'raxis';
	import {
		CanvasSettings,
		KeysToTrack,
		Sprite,
		Transform,
		defaultPlugins,
	} from 'raxis-plugins';

	let target: HTMLElement;

	const ecs = new ECS()
		.insertPlugins(...defaultPlugins)
		.addStartupSystem((ecs) => {
			const transform = new Transform(new Vec2(100, 100));
			transform.avel = Math.PI / 4;

			ecs.spawn(transform, new Sprite('rectangle', 'blue'));
		});

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
		display: flex;
		width: 100%;
		height: 100%;

		justify-content: center;
		align-items: center;

		div {
			width: 60%;
			height: 60%;
			background: whitesmoke;
			border: 3px solid black;
		}
	}
</style>
