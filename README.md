# Svelte Sortable

```svelte
<script>
  let items = [
    { id: 1, value: 'A' },
    { id: 2, value: 'B' },
    { id: 3, value: 'C' },
  ]
</script>

<Sortable bind:list={items} let:item let:order>
  <div>{order} -> {item.value}</div>
</Sortable>
```

## Customize element

```svelte
<table>
  <tbody>
    <Sortable bind:list={items} element="tr">
      <div>{order} -> {item.value}</div>
    </Sortable>
  </tbody>
</table>
```

## Customize class

```svelte
<Sortable bind:list={items} class="bg-blue-100">
  <div>{order} -> {item.value}</div>
</Sortable>
```

## Reorder event

```svelte
<Sortable bind:list={items} on:reorder={(e) => console.log(e.detail.source, e.detail.target)}>
  <div>{order} -> {item.value}</div>
</Sortable>
```
