<script>
	import SceneAudi from '$lib/models/audiS5/SceneAudi.svelte';
	import { Canvas } from '@threlte/core';
</script>

<section class="h-screen w-full">
	<div class="canvas-wrapper">
		<Canvas>
			<SceneAudi />
		</Canvas>
	</div>
</section>

<style>
	.canvas-wrapper {
		height: 100vh; 
	}
</style>
