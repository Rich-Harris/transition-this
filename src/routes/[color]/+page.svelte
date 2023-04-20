<script>
	import { page } from '$app/stores';
	import { Canvas } from '@threlte/core';
	import Scene from './Scene.svelte';
</script>

<Canvas>
	<Scene color={$page.params.color} />
</Canvas>
