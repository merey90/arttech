<script lang="ts">
	import OrkhonText from '../components/OrkhonText.svelte';
	import ConstructionImage from '$lib/images/construction.png';

	export let show: boolean = true; // Prop to control the visibility of the component
</script>

{#if show}
	<div class="construction-overlay">
		<div class="construction-container">
			<div class="message-container">
				<h2><OrkhonText text="Site under construction" intervalTime={100} totalTime={500} /></h2>
				<p>
					<OrkhonText
						text="Our garden is still growing! 🌱 We're busy planting the seeds for a beautiful website.
					Check back soon to see what's blooming! 🌸"
						intervalTime={50}
						totalTime={1000}
					/>
				</p>
			</div>
		</div>
	</div>
{/if}

<style>
	.construction-overlay {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, 0.7);
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1000;
	}

	.construction-container {
		background-color: rgba(0, 0, 0, 0.5);
		padding: 20px;
		border-radius: 5px;
		display: flex;
		max-width: 800px; /* Adjust as needed */
	}

	.image-container {
		width: 200px; /* Adjust as needed */
		margin-right: 20px;
	}

	.image-container img {
		width: 100%;
		height: auto;
		border-radius: 5px;
	}

	.message-container {
		text-align: center;
	}

	h2 {
		margin-bottom: 10px;
		font-family: 'Playfair Display', serif; /* Example of a creative serif font */
		font-size: 2.5em;
		font-weight: 700;
		letter-spacing: 2px;
		color: rgb(176, 252, 89);
	}

	p {
		font-family: 'Roboto', sans-serif; /* Example of a clean sans-serif font */
		font-size: 1.2em;
		line-height: 1.6;
		color: rgb(176, 252, 89);
	}
</style>
