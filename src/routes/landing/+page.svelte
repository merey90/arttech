<script lang="ts">
	import { fade, fly, slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import { onMount } from 'svelte';

	// Sample data for testimonials (replace with your actual data)
	const testimonials = [
		{
			quote: "This is the best website I've ever seen! It's so clean and easy to use.",
			author: 'John Doe'
		},
		{
			quote: 'I was amazed by the beautiful design and smooth animations.',
			author: 'Jane Smith'
		}
	];

	let visible = false;

	onMount(() => {
		visible = true;
	});
</script>

{#if visible}
	<section id="hero" in:fade>
		<h2>Welcome to Our Website</h2>
		<p>This is an advanced landing page built with Svelte.</p>
		<button>Learn More</button>
	</section>

	<section id="features" in:fade>
		<h2>Our Features</h2>
		<div class="features-grid">
			<div
				class="feature fly-up"
				transition:fly={{
					delay: 250,
					duration: 300,
					x: 100,
					y: 500,
					opacity: 0.5,
					easing: quintOut
				}}
			>
				<h3>Feature 1</h3>
				<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
			</div>
			<div
				class="feature fly-up"
				transition:fly={{
					delay: 500,
					duration: 300,
					x: 100,
					y: 500,
					opacity: 0.5,
					easing: quintOut
				}}
			>
				<h3>Feature 2</h3>
				<p>Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
			</div>
			<div
				class="feature fly-up"
				transition:fly={{
					delay: 750,
					duration: 300,
					x: 100,
					y: 500,
					opacity: 0.5,
					easing: quintOut
				}}
			>
				<h3>Feature 3</h3>
				<p>Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.</p>
			</div>
		</div>
	</section>

	<section id="about" in:fade>
		<h2>About Us</h2>
		<p>
			We are a team of passionate individuals who love to create beautiful and functional websites.
		</p>
	</section>

	<section id="testimonials" in:fade>
		<h2>Testimonials</h2>
		<div class="testimonials-grid">
			{#each testimonials as testimonial (testimonial.quote)}
				<div class="testimonial slide-in" in:slide={{ duration: 500, delay: 200, axis: 'x' }}>
					<p>{testimonial.quote}</p>
					<p>- {testimonial.author}</p>
				</div>
			{/each}
		</div>
	</section>

	<section id="team" in:fade>
		<h2>Our Team</h2>
		<div class="team-grid">
			<div class="team-member slide-in" in:slide={{ axis: 'x', duration: 500, delay: 200 }}>
				<img src="team-member-1.jpg" alt="Team Member 1" />
				<h3>John Doe</h3>
				<p>CEO</p>
			</div>
			<div class="team-member slide-in" in:slide={{ axis: 'x', duration: 500, delay: 200 }}>
				<img src="team-member-1.jpg" alt="Team Member 1" />
				<h3>MMM AAA</h3>
				<p>CEO</p>
			</div>
		</div>
	</section>

	<section id="contact" in:fade>
		<h2>Contact Us</h2>
		<p>Have a question or want to collaborate? Get in touch!</p>
		<button>Contact</button>
	</section>
{/if}

<style>
	section {
		padding: 80px 20px;
		text-align: center;
	}

	h2 {
		font-size: 2.5em;
		margin-bottom: 20px;
		color: var(--primary-color);
	}

	p {
		font-size: 1.2em;
		line-height: 1.6;
		color: #555;
	}

	button {
		background-color: var(--secondary-color);
		color: white;
		padding: 12px 20px;
		border: none;
		border-radius: 5px;
		font-size: 1em;
		cursor: pointer;
		transition: background-color 0.3s ease;
	}

	button:hover {
		background-color: #c0392b; /* Darker shade on hover */
	}

	/* Section-Specific Styling */
	#hero {
		background-color: #f4f4f4;
		min-height: 400px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	#features {
		background-color: white;
	}

	.feature {
		display: inline-block;
		width: calc(33.33% - 20px); /* Adjust for spacing */
		margin: 10px;
		vertical-align: top;
	}

	#about {
		background-color: #f9f9f9;
	}

	#contact {
		background-color: white;
	}

	#testimonials {
		background-color: #f4f4f4;
	}

	.testimonial {
		display: inline-block;
		width: calc(50% - 20px);
		margin: 10px;
		vertical-align: top;
		padding: 20px;
		border-radius: 5px;
		box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
		background-color: white;
	}

	.testimonial p {
		font-style: italic;
		margin-bottom: 15px;
	}

	/* Team Section */
	#team {
		background-color: white;
	}

	.team-member {
		display: inline-block;
		width: calc(25% - 20px);
		margin: 10px;
		vertical-align: top;
		text-align: center;
	}

	.team-member img {
		width: 100px;
		height: 100px;
		border-radius: 50%;
		object-fit: cover;
	}
</style>
