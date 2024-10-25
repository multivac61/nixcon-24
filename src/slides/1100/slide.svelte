<script>
	import Snow from '$lib/snow.svelte'
	import { Transition } from '@animotion/core'
</script>

<Snow />

<Transition class="mt-16">
	<h1 class="text-8xl">Thank yous</h1>
	<ul class="mt-8 flex min-w-[1000px] flex-col gap-8 text-left">
		<Transition><li>NixOS Organizers</li></Transition>
		<Transition><li>Nix community 🫶</li></Transition>
		<Transition><li>Matt Croughan</li></Transition>
		<Transition><li>Genki team</li></Transition>
		<Transition><li>Andrea ❤️</li></Transition>
	</ul>
</Transition>
