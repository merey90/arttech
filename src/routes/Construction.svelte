<script lang="ts">
	import { browser } from '$app/environment';
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';
	import OrkhonText from '../components/OrkhonText.svelte';
	import ProjectList from '../components/ProjectList.svelte';

	export let show: boolean = true;

	// Create a writable store for window width
	const windowWidth = writable(browser ? window.innerWidth : 0);

	// Function to update store on resize
	const updateWidth = () => {
		if (browser) {
			windowWidth.set(window.innerWidth);
		}
	};

	// Set up event listener
	onMount(() => {
		if (browser) {
			window.addEventListener('resize', updateWidth);
			updateWidth(); // Set initial value
			return () => window.removeEventListener('resize', updateWidth);
		}
	});

	// Reactive variables
	$: isMobile = $windowWidth < 768;

	$: descriptionText =
		"Our garden is still growing! We're busy planting the seeds for a beautiful website. \nCheck back soon to see what's blooming!";
</script>

{#if show}
	<div class="construction-overlay">
		<div class="construction-container {isMobile ? 'mobile' : ''}">
			<div class="message-container">
				<h2>
					<OrkhonText text="ArtTech Garden" intervalTime={50} totalTime={1000} />
				</h2>
				<div class="description">
					<OrkhonText text={descriptionText} intervalTime={50} totalTime={4000} />
				</div>
			</div>
		</div>
		<div class="construction-container {isMobile ? 'mobile' : ''}">
			<div class="message-container">
				<ProjectList />
			</div>
		</div>
	</div>
{/if}

<style>
	.construction-overlay {
		overflow-y: auto;
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1000;
		flex-direction: column;
	}

	.construction-container {
		padding: 20px;
		border-radius: 5px;
		display: flex;
		max-width: 1000px;
		&:not(.mobile) {
			background-color: rgba(0, 0, 0, 0.5);
		}
		margin-bottom: 20px;
	}

	.message-container {
		text-align: center;
	}

	.description {
		line-height: 30px;
		font-family: 'Lucida console', 'Apple Color Emoji', 'Noto Color Emoji', sans-serif;
		font-size: 1.2em;
		line-height: 1.6;
		color: rgb(176, 252, 89);
	}

	h2 {
		margin-bottom: 10px;
		font-family: 'Lucida console', 'Apple Color Emoji', 'Noto Color Emoji', sans-serif;
		font-size: 2.3em;
		font-weight: 700;
		letter-spacing: 2px;
		color: rgb(176, 252, 89);
		padding-bottom: 15px;
		line-height: 1.8;
	}
</style>
