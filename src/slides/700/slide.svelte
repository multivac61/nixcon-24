<script lang="ts">
	import { Code, Action, Transition } from '@animotion/core'

	let code: ReturnType<typeof Code>
	let text: HTMLElement
</script>

<Transition>
	<code bind:this={text} class="mp-8 text-8xl font-bold drop-shadow-sm">$ nix flake check</code>
</Transition>

<Transition
	do={async () => {
		text.classList.replace('text-8xl', 'text-6xl')
	}}
	class="mt-16"
>
	<ul class="text-md flex min-w-4xl flex-col gap-8 text-left">
		<Transition><li>Makes sure <span class="font-bold">everything</span> builds</li></Transition>
		<Transition><li>Runs tests locally</li></Transition>
		<Transition><li><code>treefmt</code> for formatting, linting...</li></Transition>
	</ul>
</Transition>
