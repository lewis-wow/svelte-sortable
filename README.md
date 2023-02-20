# Svelte Sortlist

## Installation

```bash
npm i svelte-sortlist
```

List must be `let`, it cannot be `const` if you bind it. Cause inside `SortList` component it will change.

```svelte
<script>
  import SortList from 'svelte-sortlist'

  let items = [
    { id: 1, value: 'A' },
    { id: 2, value: 'B' },
    { id: 3, value: 'C' },
  ]
</script>

<SortList bind:list={items} let:item let:index>
  <div>{index} -> {item.value}</div>
</SortList>
```

## Customize element

You can customize `SortList` element with element prop. It cannot be component.

```svelte
<table>
  <tbody>
    <SortList bind:list={items} element="tr" let:item>
      <div>{item.value}</div>
    </SortList>
  </tbody>
</table>
```

## Customize class

You can specify class of SortList. So you can use it with Tailwind.

```svelte
<SortList bind:list={items} class="bg-blue-100" let:item>
  <div>{item.value}</div>
</SortList>
```

## Reorder event

With bindings you don't need this event, cause your items will be synced thanks to bind. But if you want for example sync it with backend server, you can use the reorder event and request the server on each reorder.

```svelte
<SortList bind:list={items} let:item on:reorder={(e) => console.log(e.detail.source, e.detail.target)}>
  <div>{item.value}</div>
</SortList>
```

## If is over the item

You can for example apply styles on element that you are hovering over.

```svelte
<SortList bind:list={items} let:item let:isOver>
  <div>{isOver ? 'over' : 'not over'} - {item.value}</div>
</SortList>
```

## Rest props

`SortList` can be extended by any props. For example `id="my-id"`.
