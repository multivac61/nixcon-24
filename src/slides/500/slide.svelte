<script lang="ts">
	import { Transition } from '@animotion/core'
	let video: HTMLVideoElement
</script>

<!-- svelte-ignore a11y_media_has_caption -->
<video bind:this={video} class="pointer-events-none">
	<source src="sineater.webm" />
</video>

<Transition
	do={async () => {
		await video.play()
	}}
></Transition>
