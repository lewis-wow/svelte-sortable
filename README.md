# Svelte Sortable

```svelte
<script>
  let items = [
    { id: 1, value: 'A' },
    { id: 2, value: 'B' },
    { id: 3, value: 'C' },
  ]
</script>

<Sortable bind:list={items} let:item let:index>
  <div>{index} -> {item.value}</div>
</Sortable>
```

## Customize element

```svelte
<table>
  <tbody>
    <Sortable bind:list={items} element="tr" let:item>
      <div>{item.value}</div>
    </Sortable>
  </tbody>
</table>
```

## Customize class

```svelte
<Sortable bind:list={items} class="bg-blue-100" let:item>
  <div>{item.value}</div>
</Sortable>
```

## Reorder event

```svelte
<Sortable bind:list={items} let:item on:reorder={(e) => console.log(e.detail.source, e.detail.target)}>
  <div>{item.value}</div>
</Sortable>
```

## If is over the item

You can for example apply styles on element that you are hovering over.

```svelte
<Sortable bind:list={items} let:item let:isOver>
  <div>{isOver ? 'over' : 'not over'} - {item.value}</div>
</Sortable>
```
