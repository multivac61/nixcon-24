<script lang="ts">
	import { Transition } from '@animotion/core'
</script>

<Transition class="my-16">
	<code>$ nix flake check</code>
	<ul class="text-md mt-8 flex min-w-[1000px] flex-col gap-8 text-left">
		<Transition><li>Builds <span class="font-bold">everything</span></li></Transition>
		<Transition><li><code>nix fmt</code> for formatting, <code>treefmt</code> for linting...</li></Transition>
		<Transition><li>Runs tests</li></Transition>
	</ul>
	<Transition class="mt-16">... rest done in impure effects</Transition>
</Transition>
