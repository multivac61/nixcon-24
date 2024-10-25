<script lang="ts">
	import { Transition } from '@animotion/core'

	let text: HTMLElement
</script>

<code bind:this={text} class="mt-16 text-6xl font-bold drop-shadow-sm">$ whoami</code>
<Transition>
	<ul class="mt-16 flex min-w-[1000px] flex-col gap-8 text-left">
		<Transition><li>Óli 👋</li></Transition>
		<Transition><li>Writing firmware (ASM, C, C++, Rust) for 9+ years</li></Transition>
		<Transition><li>Nix enthusist for 2+ years</li></Transition>
		<Transition><li>Building Genki for 10+ years</li></Transition>
		<Transition><li>🇮🇸 for 32+ years</li></Transition>
	</ul>
</Transition>
