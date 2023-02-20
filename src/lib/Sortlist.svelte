<script lang="ts">
	import { createEventDispatcher } from 'svelte'
	import { flip } from 'svelte/animate'
	type T = $$Generic

	interface ListItem {
		id: string | number
		value: T
	}

	interface Source {
		id: string | number
		order: number
	}

	export let list: ListItem[]
	export let element = 'div'
	export let disabled = false
	export let animation = true
	let className = ''
	export { className as class }
	export let style = ''

	const dispatch = createEventDispatcher()

	let source: Source | null = null
	let isOver: string | number | null = null

	const start = (e: DragEvent, id: string | number) => {
		e.dataTransfer?.clearData()
		e.dataTransfer?.setData('text/plain', id.toString())
	}

	const over = (target: Source) => isOver !== target.id && (isOver = target.id)
	const leave = () => isOver = null

	const reorder = (source: Source | null, target: Source | null) => {
		if (disabled || !source || !target) return
		if (source.id === target.id) return

		const { order: sourceIndex } = source
		const { order: targetIndex } = target

		isOver = null

		list[sourceIndex] = [list[targetIndex], (list[targetIndex] = list[sourceIndex])][0]
		list = list

		dispatch('reorder', { source, target })
	}
</script>

{#each list as item, order (item.id)}
	<svelte:element
		this={element}
		draggable={!disabled}
		class={className}
		{style}
		{...$$restProps}
		on:dragstart={(e) => (source = { order, id: item.id }) && start(e, source.id)}
		on:dragover|preventDefault={() => over({ order, id: item.id })}
		on:dragleave={leave}
		on:dragenter|preventDefault={() => null}
		on:drop|preventDefault={() => reorder(source, { order, id: item.id })}
		animate:flip={{ duration: source !== null && animation === true ? 300 : 0 }}
	>
		<slot {item} index={order} isOver={item.id === isOver} />
	</svelte:element>
{/each}
