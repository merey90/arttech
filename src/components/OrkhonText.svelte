<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	// Input text
	export let text: string = 'Hello Svelte World with multiple   spaces!';

	// Interval at which letters are replaced with runes
	export let intervalTime: number = 50;

	// How long to randomize before showing the final text
	export let totalTime: number = 2000;

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

	// We'll store the randomized display tokens here. Each token is either:
	// - A "word" (array of characters)
	// - A "space" (string of spaces)
	//
	// Example: "Hello   World" -> tokens: ["Hello", "   ", "World"]
	type Token = {
		type: 'word' | 'space';
		content: string[] | string; // array of chars if "word", or string if "space"
	};

	let displayTokens: Token[] = [];

	let interval: number | undefined;

	// Random rune
	function getRandomRune(): string {
		return orkhonRunes[Math.floor(Math.random() * orkhonRunes.length)];
	}

	// Splits text into tokens capturing the spaces as separate entries.
	function tokenize(input: string): Token[] {
		// This regex splits on ANY sequence of whitespace, capturing them as separate tokens.
		// So "Hello   World" => ["Hello", "   ", "World"]
		const parts = input.split(/(\s+)/);

		return parts
			.filter((part) => part.length > 0) // remove empty strings if any
			.map((part) => {
				if (/\s+/.test(part)) {
					// It's purely spaces
					return { type: 'space', content: part } as Token;
				} else {
					// It's a word (non-space)
					// We'll treat "word" content as an array of single characters
					return { type: 'word', content: part.split('') } as Token;
				}
			});
	}

	onMount(() => {
		const start = Date.now();

		// First, parse the text into tokens of words/spaces
		const tokens = tokenize(text);

		// Initialize displayTokens to random runes (for letters in each word),
		// but keep spaces as is.
		displayTokens = tokens.map((token) => {
			if (token.type === 'space') {
				// Keep spaces exactly
				return { type: 'space', content: token.content };
			} else {
				// Word: randomize each character
				const content = (token.content as string[]).map(() => getRandomRune());
				return { type: 'word', content };
			}
		});

		// Start updating
		interval = window.setInterval(() => {
			const elapsed = Date.now() - start;
			if (elapsed >= totalTime) {
				// Reveal the actual text
				displayTokens = tokens;
				clearInterval(interval);
			} else {
				// Keep randomizing for words
				displayTokens = displayTokens.map((t, i) => {
					if (tokens[i].type === 'space') {
						// Preserve spaces
						return { type: 'space', content: tokens[i].content };
					} else {
						// Re-randomize each character in the word
						const newChars = (t.content as string[]).map((_, idx) => getRandomRune());
						return { type: 'word', content: newChars };
					}
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

<!-- 
  RENDERING:
  - If token is "space", just output the space string directly.
  - If token is "word", we wrap the entire word in .word so the browser 
    doesn't break lines in the middle of the word. 
  - Each letter in the word is given .letter with a fixed width, to avoid jumpiness.
-->
<div class="orkhon-text">
	{#each displayTokens as token}
		{#if token.type === 'space'}
			{@html token.content} <!-- just output the spaces -->
		{:else}
			<!-- entire word is an inline-block so it can break only between words -->
			<span class="word">
				{#each token.content as char}
					<span class="letter">{char}</span>
				{/each}
			</span>
		{/if}
	{/each}
</div>

<style>
	/* If you want to allow line wrapping between words (but not in the middle), 
     use white-space: normal (or pre-wrap if you have newlines). */
	.orkhon-text {
		/* 
      'white-space: normal' allows wrapping between .word containers 
      or after spaces. 
    */
		white-space: normal;

		/* or 'pre-wrap' if you need to preserve any actual line breaks 
       typed into the text, but still allow wrapping: 
       white-space: pre-wrap;
    */

		/* 
      If you have extremely long words that won't fit on a single line, 
      you'll still get overflow or the user must scroll horizontally. 
      (Because there's nowhere valid to break within that word container.)
    */
	}

	/* Each word is an inline-block, so the browser can't break in the middle of it. */
	.word {
		display: inline-block;
	}

	/* Each letter has a fixed width, so it won't cause jumpiness when it changes shape. */
	.letter {
		display: inline-block;
		width: 1ch;
		text-align: center;
	}
</style>
