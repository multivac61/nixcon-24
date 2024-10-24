<script lang="ts">
	import { Transition } from '@animotion/core'

	let text: HTMLParagraphElement
	let list: HTMLUListElement
</script>

<Transition
	do={async () => {
		text.classList.replace('text-6xl', 'text-8xl')
	}}
>
	<p bind:this={text} class="text-8xl font-bold drop-shadow-sm">Why Nix?</p>
</Transition>

<Transition
	do={async () => {
		text.classList.replace('text-8xl', 'text-6xl')
	}}
	class="mt-16"
></Transition>

<ul bind:this={list} class="flex min-w-2xl flex-col gap-8 text-left">
	<Transition><li>For the environments!</li></Transition>
	<Transition><li>Deterministic* builds</li></Transition>
	<Transition><li>"It's good for you"</li></Transition>
	<Transition><li>Sin-eater</li></Transition>
</ul>
