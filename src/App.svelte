<script>
	import Sortable from './lib/Sortable.svelte';

	let list = [
		{ id: 1, value: 'A' },
		{ id: 2, value: 'B' },
		{ id: 3, value: 'C' },
	]
</script>

<main>
	<Sortable bind:list let:item on:reorder={(e) => console.log(e.detail.source)}>
		<div>{item.value}</div>
	</Sortable>
</main>
