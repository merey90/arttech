<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	// Props
	export let text: string = 'Hello, Svelte!';
	export let intervalTime: number = 50; // How often to update the runes (ms)
	export let totalTime: number = 2000; // How long until we reveal the text (ms)

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

	let displayText: string = '';
	let interval: number | undefined;

	onMount(() => {
		const start = Date.now();

		interval = window.setInterval(() => {
			if (Date.now() - start >= totalTime) {
				displayText = text; // Reveal the actual text
				clearInterval(interval);
			} else {
				// For each non-space character, display a random rune
				displayText = text
					.split('')
					.map((char) =>
						char === ' ' ? ' ' : orkhonRunes[Math.floor(Math.random() * orkhonRunes.length)]
					)
					.join('');
			}
		}, intervalTime);
	});

	onDestroy(() => {
		if (interval) clearInterval(interval);
	});
</script>

<span>{displayText}</span>
