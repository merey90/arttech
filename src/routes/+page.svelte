<script lang="ts">
	import Construction from './Construction.svelte';

	let activeElement: string | null = null;

	const handleClick = (element: string) => {
		activeElement = activeElement === element ? null : element;
	};
</script>

<svelte:head>
	<title>ArtTech</title>
	<meta name="description" content="Home page" />
</svelte:head>

<Construction show={true} />
<div class="container">
	<button class="body-part" on:click={() => handleClick('eyes')}>
		<div class="line"></div>
		<div class="label">See</div>
	</button>

	<button class="body-part" on:click={() => handleClick('mouth')}>
		<div class="line"></div>
		<div class="label">Talk</div>
	</button>

	<button class="body-part" on:click={() => handleClick('ears')}>
		<div class="line"></div>
		<div class="label">Hear</div>
	</button>

	<button class="body-part" on:click={() => handleClick('hands')}>
		<div class="line"></div>
		<div class="label">Make</div>
	</button>

	<button class="body-part" on:click={() => handleClick('foot')}>
		<div class="line"></div>
		<div class="label">Follow</div>
	</button>
</div>

<style>
	.container {
		display: flex;
		justify-content: center;
		align-items: center;
		min-height: 100vh;
		background-image: url('$lib/images/main.png');
		background-size: cover;
		background-position: center;
		flex-direction: column;
		gap: 40px;
		font-family: sans-serif;
	}

	.body-part {
		position: relative;
		cursor: pointer;
		display: flex;
		align-items: center;
		border: none;
		background-color: rgba(0, 0, 0, 0.7);
	}

	.line {
		width: 100px;
		height: 2px;
		background-color: white;
		margin-right: 10px;
		transition: transform 0.3s ease;
	}

	.body-part:hover .line {
		transform: scaleX(1.2);
	}

	.label {
		font-size: 1.2em;
		font-weight: bold;
		color: white;
		transition: opacity 0.3s ease;
		opacity: 0.8;
	}

	.body-part:hover .label {
		opacity: 1;
	}
</style>
