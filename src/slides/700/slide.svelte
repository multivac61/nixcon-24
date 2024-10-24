<script lang="ts">
	import { Code, Transition } from '@animotion/core'

	let code: ReturnType<typeof Code>
</script>

<Code bind:this={code} lang="shellsession" theme="catppuccin-mocha" code={`$ nix flake check`} options={{ duration: 1000, stagger: 0.3, containerStyle: false }} />

<Transition class="mt-16">
	<ul class="text-md flex min-w-4xl flex-col gap-8 text-left">
		<Transition><li>Builds <span class="font-bold">everything</span></li></Transition>
		<Transition><li>Runs tests</li></Transition>
		<Transition><li><code>treefmt</code> for formatting, linting...</li></Transition>
	</ul>
</Transition>
