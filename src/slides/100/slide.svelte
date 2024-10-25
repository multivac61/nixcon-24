<script lang="ts">
	import { Transition } from '@animotion/core'
	import { onMount } from 'svelte'
	let y = $state(0)

	onMount(() => {
		setInterval(() => {
			y = Math.sin(Date.now() / 500) * 10
		}, 16)
	})

	let text: HTMLParagraphElement
</script>

<Transition><h1 bind:this={text} class=" flex items-center justify-center text-8xl font-bold drop-shadow-sm">Deterministic* Firmware in Nix</h1></Transition>

<Transition class="mt-32">
	<img src="nixcon24.svg" style:transform="translateY({y}px)" style:transition="transform 0.1s ease-out" alt="Floating" />
</Transition>
