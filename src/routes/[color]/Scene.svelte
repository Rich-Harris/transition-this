<script>
	import { page } from '$app/stores';
	import * as THREE from 'three';
	import { T, useFrame } from '@threlte/core';
	import { interactivity } from '@threlte/extras';
	import { spring, tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
	import { afterNavigate } from '$app/navigation';

	interactivity();

	const color = tweened($page.params.color, {
		duration: 600,
		easing: cubicOut,
		interpolate: (a, b) => {
			const from = new THREE.Color(a);
			const to = new THREE.Color(b);
			const lerped = new THREE.Color(a);

			return (t) => {
				lerped.lerpColors(from, to, t);
				return lerped.getStyle();
			};
		}
	});

	const x = spring();
	const y = spring();
	const z = spring();
	const box_scale = spring();
	const group_scale = spring(1);

	let rotation = 0;

	useFrame((state, delta) => {
		rotation += delta * 0.1;
	});

	afterNavigate(() => {
		x.set(Math.random() * Math.PI * 2);
		y.set(Math.random() * Math.PI * 2);
		z.set(Math.random() * Math.PI * 2);
		box_scale.set(Math.random() + 0.5);
		color.set($page.params.color);
	});
</script>

<T.PerspectiveCamera
	makeDefault
	position={[5, 5, 5]}
	on:create={({ ref }) => {
		ref.lookAt(0, 1, 0);
	}}
/>

<T.DirectionalLight position={[3, 10, 7]} />

<T.Group rotation.y={rotation} position.y={1} scale={$group_scale}>
	<T.Mesh
		rotation={[$x, $y, $z]}
		scale={$box_scale}
		on:pointerenter={() => group_scale.set(1.5)}
		on:pointerleave={() => group_scale.set(1)}
	>
		<T.BoxGeometry args={[1, 1, 1]} />
		<T.MeshStandardMaterial color={$color} />
	</T.Mesh>
</T.Group>
