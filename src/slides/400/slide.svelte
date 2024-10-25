<script lang="ts">
	import { Transition } from '@animotion/core'

	let text: HTMLParagraphElement
	let list: HTMLUListElement
</script>

<Transition>
	<p bind:this={text} class="text-8xl font-bold drop-shadow-sm">Why Nix?</p>
	<ul bind:this={list} class="mt-16 flex min-w-[1000px] flex-col gap-8 text-left">
		<Transition><li>For the environments!</li></Transition>
		<Transition><li>Deterministic* builds</li></Transition>
		<Transition><li>"It's good for you"</li></Transition>
		<Transition><li>Gives you closure</li></Transition>
		<Transition><li><code>nixpkgs</code> is sin-eater of open source world</li></Transition>
	</ul>
</Transition>
