<script lang="ts">
	import { Transition } from '@animotion/core'

	let text: HTMLParagraphElement
	let viktor: HTMLVideoElement
	let pedro: HTMLImageElement
</script>

<Transition><p bind:this={text} class="text-8xl font-bold drop-shadow-sm">Genki?</p></Transition>

<Transition
	do={async () => {
		text.classList.replace('text-8xl', 'text-6xl')
	}}
	class="mt-16"
>
	<img bind:this={pedro} src="pedro.jpeg" class="max-w-md" alt="" />
	<!-- svelte-ignore a11y_media_has_caption -->
	<video bind:this={viktor} hidden class="pointer-events-none">
		<source src="viktor.mp4" type="video/webm" />
	</video>
</Transition>

<Transition
	do={async () => {
		pedro.hidden = true
		viktor.hidden = false
		await viktor.play()
	}}
></Transition>
