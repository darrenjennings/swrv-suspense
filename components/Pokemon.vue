<template>
  <div>
    <a :href="data.url">{{data.name}}</a>
  </div>
</template>

<script lang="ts">
import useSWRV from "swrv";
import { defineComponent } from "vue";

interface Pokemon {
  url: string;
}

export default defineComponent({
  props: {
    pokeIndex: {
      type: Number,
      required: true
    },
  },
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
    };
  },
});
</script>

<style scoped>
</style>
