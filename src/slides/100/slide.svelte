<script lang="ts">
	import { Transition } from '@animotion/core'

	let text: HTMLParagraphElement
</script>

<p bind:this={text} class="text-8xl font-bold drop-shadow-sm">Deterministic Firmware in Nix</p>

<Transition
	do={async () => {
		text.textContent = 'Deterministic* Firmware in Nix'
	}}
></Transition>

<Transition
	do={async () => {
		text.classList.replace('text-8xl', 'text-6xl')
	}}
	class="mt-16"
>
	<img class="drop-shadow-md" src="nix.svg" alt="Nix logo" />
</Transition>
