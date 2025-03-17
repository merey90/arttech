<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	// Props
	export let text: string = 'Hello 🌱🌸 Svelte!';
	export let intervalTime: number = 50; // ms between random updates
	export let totalTime: number = 2000; // ms until revealing real text

	// Full set of Orkhon runes
	const orkhonRunes: string[] = [
		'𐰀',
		'𐰁',
		'𐰂',
		'𐰃',
		'𐰄',
		'𐰅',
		'𐰆',
		'𐰇',
		'𐰈',
		'𐰉',
		'𐰊',
		'𐰋',
		'𐰌',
		'𐰍',
		'𐰎',
		'𐰏',
		'𐰐',
		'𐰑',
		'𐰒',
		'𐰓',
		'𐰔',
		'𐰕',
		'𐰖',
		'𐰗',
		'𐰘',
		'𐰙',
		'𐰚',
		'𐰛',
		'𐰜',
		'𐰝',
		'𐰞',
		'𐰟',
		'𐰠',
		'𐰡',
		'𐰢',
		'𐰣',
		'𐰤',
		'𐰥',
		'𐰦',
		'𐰧',
		'𐰨',
		'𐰩',
		'𐰪',
		'𐰫',
		'𐰬',
		'𐰭',
		'𐰮',
		'𐰯',
		'𐰰',
		'𐰱',
		'𐰲',
		'𐰳',
		'𐰴',
		'𐰵',
		'𐰶',
		'𐰷',
		'𐰸',
		'𐰹',
		'𐰺',
		'𐰻',
		'𐰼',
		'𐰽',
		'𐰾',
		'𐰿',
		'𐱀',
		'𐱁',
		'𐱂',
		'𐱃',
		'𐱄',
		'𐱅',
		'𐱆',
		'𐱇',
		'𐱈'
	];

	// We'll hold the currently displayed characters here
	let displayChars: string[] = [];

	let interval: number | undefined;

	// Helper to detect emojis (we'll allow all Extended Pictographic codepoints)
	// Modern browsers support this Unicode property-based regex:
	function isEmoji(char: string): boolean {
		// If your environment lacks full Unicode regex support, see alternative approaches.
		return /\p{Extended_Pictographic}/u.test(char);
	}

	// Return a random Orkhon rune
	function getRandomRune(): string {
		return orkhonRunes[Math.floor(Math.random() * orkhonRunes.length)];
	}

	onMount(() => {
		const start = Date.now();

		// Initialize displayChars
		displayChars = text.split('').map((ch) => {
			if (ch === ' ' || isEmoji(ch)) {
				// Keep spaces and emojis from the start
				return ch;
			}
			// Everything else is replaced with a random rune
			return getRandomRune();
		});

		// Update runes on interval until totalTime elapses
		interval = window.setInterval(() => {
			const elapsed = Date.now() - start;
			if (elapsed >= totalTime) {
				// Reveal the actual text
				displayChars = text.split('');
				clearInterval(interval);
			} else {
				// Keep re-randomizing for non-space, non-emoji characters
				displayChars = displayChars.map((current, i) => {
					const original = text[i];
					// If space or emoji, do not randomize
					if (original === ' ' || isEmoji(original)) {
						return original;
					}
					// Otherwise randomize
					return getRandomRune();
				});
			}
		}, intervalTime);
	});

	onDestroy(() => {
		if (interval !== undefined) {
			clearInterval(interval);
		}
	});
</script>

<!-- We wrap all letters in a container with white-space: pre
     so that spaces are preserved as-is. -->
<span class="orkhon-text">
	{#each displayChars as char}
		{char}
	{/each}
</span>
