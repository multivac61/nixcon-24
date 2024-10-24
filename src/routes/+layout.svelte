<script lang="ts">
	import '../styles/app.css'

	let { children } = $props()
</script>

<svelte:head>
	<title>Deterministic* Firmware in Nix</title>
</svelte:head>

{@render children()}

