<script>
	import { OrbitControls, Environment, HTML, GLTF } from '@threlte/extras';
	import { T } from '@threlte/core';
	import RetroAudi from './RetroAudi.svelte';
	import { Color } from 'three';
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';

	let carComponent;

	function handleDrive() {
		if (carComponent) {
			carComponent.driveForward();
		}
	}

	let colorIndex = 0;
	let loadedGltf;

	const colors = [
		new Color(0xff0000),
		new Color(0x00ff00),
		new Color(0x0000ff),
		new Color(0xffffff)
	]; // Add more colors as needed

	// Create a tweened store for the car color
	const carColor = tweened(new Color(0xffffff), {
		duration: 500,
		easing: cubicOut
	});

	$: if (loadedGltf && loadedGltf.materials) {
		console.log('Materials loaded:', Object.keys(loadedGltf.materials));
		// Don't change color immediately here
	}

	function toggleColor() {
		console.log('Toggle color function called');
		if (loadedGltf && loadedGltf.materials) {
			colorIndex = (colorIndex + 1) % colors.length; // Cycle through colors
			const newColor = colors[colorIndex];

			// Animate the color change
			carColor.set(newColor);

			const materialName = 'AudiS5coupe09_carpaint';
			if (loadedGltf.materials[materialName]) {
				carColor.subscribe((color) => {
					loadedGltf.materials[materialName].color = color;
					console.log(`Changed color of ${materialName} to:`, color);
				});
			}
		}
	}
</script>

<T.PerspectiveCamera makeDefault position={[50, 5, 5]} fov={75}>
	<OrbitControls />
</T.PerspectiveCamera>

<T.Group position={[0, 0, -10]} scale={0.15}>
	<GLTF
		url="/audi_s5_retro-transformed.glb"
		useDraco={true}
		bind:gltf={loadedGltf}
		on:error={(e) => {
			console.error('Error loading model:', e.detail);
		}}
	/>
</T.Group>
<Environment path="hdr" format="hdr" isBackground={false} files="metro_noord_1k.hdr" />

<T.Group position={[0, 5, 0]}>
	<HTML transform>
		<button on:click={toggleColor}>Toggle Car Color</button>
	</HTML>
</T.Group>

<style>
	button {
		padding: 10px 20px;
		background-color: #4caf50;
		color: white;
		border: none;
		border-radius: 5px;
		cursor: pointer;
		font-size: 16px;
	}

	button:hover {
		background-color: #45a049;
	}
</style>
