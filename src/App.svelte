<script>
	import Sortable from './lib/Sortable.svelte';

	let list = [
		{ id: 1, value: 'A' },
		{ id: 2, value: 'B' },
		{ id: 3, value: 'C' },
	]
</script>

<main>
	<Sortable bind:list let:item let:isOver>
		{isOver ? 'over' : 'not over'}
		<div style="background-color: blue;">{item.value}</div>
	</Sortable>
</main>
