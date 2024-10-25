<script lang="ts">
	import { Transition } from '@animotion/core'

	let text: HTMLParagraphElement
	let audio: HTMLAudioElement

	import { onMount, onDestroy } from 'svelte'

	let elapsed = $state(0)
	let started = $state(false)
	let duration = $state(120000)

	onMount(() => {
		let last_time = performance.now()

		let frame = requestAnimationFrame(function update(time) {
			frame = requestAnimationFrame(update)

			if (started) elapsed += Math.min(time - last_time, duration - elapsed)
			last_time = time
		})

		return () => {
			cancelAnimationFrame(frame)
		}
	})
</script>

<div class="flex flex-col gap-8">
	<h1 bind:this={text} class=" flex items-center justify-center text-8xl font-bold drop-shadow-sm">First we stretch 🤸</h1>

	<div><span class="font-mono">{((duration - elapsed) / 1000).toFixed(1)}</span>s</div>
</div>

<Transition
	do={async () => {
		started = true
		audio.play()
	}}
></Transition>

<audio bind:this={audio}>
	<source src="lilla.mp3" type="audio/mpeg" />
</audio>
