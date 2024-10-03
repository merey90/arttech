<script lang="ts">
</script>

<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class="about-page">
	<h1>About Arttech</h1>
	<p>
		Welcome to Arttech, a space where <span class="highlight">art and technology converge</span> to create
		something new and exciting.
	</p>
	<p>
		We believe that the fusion of artistic expression and technological innovation can lead to <span
			class="highlight">unprecedented forms of creativity and experiences</span
		>.
	</p>
	<p>
		At Arttech, you'll find a platform to explore the <span class="highlight"
			>intersection of art and technology</span
		>, whether you're an artist, a technologist, or simply curious about the possibilities.
	</p>
	<p>
		Join us on this journey as we push the boundaries of what's possible and <span class="highlight"
			>reimagine the future of creativity</span
		>.
	</p>
</div>

<style>
	.about-page {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		min-height: 100vh;
		padding: 20px;
		background-image: url('your-background-image.jpg'); /* Replace with your image */
		background-size: cover;
		background-position: center;
		color: white; /* Adjust color as needed */
		font-family: sans-serif;
		text-align: center;
	}

	h1 {
		font-size: 3em;
		margin-bottom: 20px;
	}

	p {
		font-size: 1.2em;
		line-height: 1.6;
		margin-bottom: 10px;
	}

	.highlight {
		font-weight: bold;
	}
</style>
