<script lang="ts">
	import { Canvas } from '@threlte/core';
	import Scene from './Scene.svelte';
	import { LoaderCircle } from '@sxxov/sv/loaders';

	const replace = (node: Node, to: Node) => {
		node.parentNode?.replaceChild(to, node);
	};

	let loaded = false;
	let vrButton: HTMLButtonElement | undefined;
</script>

<div class="in">
	<div class="content">
		{#if !loaded}
			<LoaderCircle
				height={56}
				width={56}
			/>
		{/if}
		{#if vrButton}
			<div use:replace={vrButton}></div>
		{/if}
	</div>
	<Canvas
		size={{
			width: 1,
			height: 1,
		}}
	>
		<Scene
			on:loaded={({ detail: { button } }) => {
				vrButton = button;
				loaded = true;
			}}
		/>
	</Canvas>
</div>

<style lang="postcss">
	.in {
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;

		z-index: 999999999;

		& > .content {
			position: absolute;
			top: 0;
			left: 0;
			width: 100%;
			height: 100%;
			display: flex;
			align-items: center;
			justify-content: center;

			& > :global(button) {
				position: relative !important;
				left: 0 !important;
				bottom: 0 !important;
			}
		}
	}
</style>
