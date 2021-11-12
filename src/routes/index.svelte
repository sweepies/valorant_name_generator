<script>
	import { onMount } from "svelte";
	import Button from "../components/Button.svelte";

	let data;

	onMount(update);

	async function update() {
		data = null;
		const res = await fetch("/api/generate");
		data = await res.json();

		const listener = (ev) => {
			ev.clipboardData.setData('text/plain', `${data.noun}${data.name}${data.number}`)
			ev.preventDefault()
		}
		const name = document.getElementById("name");

		name.removeEventListener("copy", listener)
		name.addEventListener("copy", listener)
	}
</script>

<div class="container">
	<div class="item" id="name">
		{#if data}
			{data.noun}<span>{data.name}</span>{data.number}
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
	}

	span {
		color: rgb(180, 180, 180);
	}

	.container {
		display: flex;
		align-items: center;
		justify-content: center;
		margin-top: 30vh;
		flex-direction: column;
		align-content: space-between;
	}

	.item {
		display: flex;
		margin-bottom: 5vh;
	}
</style>
