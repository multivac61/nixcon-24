<script lang="ts">
	import { Transition } from '@animotion/core'

	let text: HTMLParagraphElement
</script>

<Transition>
	<p bind:this={text} class="text-8xl font-bold drop-shadow-sm">Who am I?</p>
</Transition>

<Transition
	do={async () => {
		text.classList.replace('text-8xl', 'text-6xl')
	}}
	class="mt-16"
>
	<ul class="flex min-w-4xl flex-col gap-8 text-left">
		<Transition><li>🇮🇸</li></Transition>
		<Transition><li>Alive for 32+ years</li></Transition>
		<Transition><li>Building Genki for 10+ years</li></Transition>
		<Transition><li>Writing firmware (ASM, C, C++, Rust) for 9+ years</li></Transition>
		<Transition><li>Nix enthusist for 2+ years</li></Transition>
	</ul>
</Transition>
