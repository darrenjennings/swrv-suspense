# swrv-suspense

## Running

```
yarn
yarn dev
```

## Notes

Using suspense boundaries with `async setup`:

```vue
<template>
  <Suspense> <!-- you can add :key="count" to force rerenders -->
    <template #default>
      <Pokemon :pokeIndex="count" />
    </template>
    <template #fallback>
      loading...
    </template>
  </Suspense>
</template>
```

Await the mutation (only makes 1 request because of in-flight promise deduplication):

```ts
interface Pokemon {
  url: string;
}

async setup(props) {
  const { data, revalidate: mutate } = useSWRV<Pokemon>(
    () => `https://pokeapi.co/api/v2/pokemon/${props.pokeIndex}`,
    (key) =>
      fetch(key)
        .then((res) => res.json())
        .then((json) => ({ ...json, url: key }))
  );
  
  await mutate()

  return {
    data
  }
}
```
