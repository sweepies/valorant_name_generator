<script>
	import { onMount } from "svelte";
	import Button from "../components/Button.svelte";

	let data;

	onMount(update);

	async function update() {
		data = null;
		const res = await fetch("/api/generate");
		data = await res.json();
	}

</script>

<div class="container">
	<div id="name">
		{#if data}
			{data.noun}<wbr><span>{data.name}</span><wbr>{data.number}
		{:else}
			...
		{/if}
	</div>
	<Button action={update} />
</div>

<style lang="scss">
	:global {
		body {
			background-color: #0f1822;
		}
	}

	@font-face {
		font-family: valorant;
		src: url('/valorant.ttf');
		font-display: swap;
	}

	#name {
		font-family: valorant, sans-serif;
		font-size: max(7vw, 5.25rem);
		color: #ff4654;
		margin-bottom: 5vh;
	}

	span {
		color: rgb(180, 180, 180);
	}

	@media (max-width: 480px) {
		#name {
			overflow-wrap: anywhere;
			font-size: 16.5vw;
		}
	}

	.container {
		display: flex;
		align-items: center;
		justify-content: center;
		margin-top: 30vh;
		flex-direction: column;
		align-content: space-between;
	}
</style>
