<template>
  <h1>Hello Vite + Vue 3!</h1>
  <p>Edit ./App.vue to test hot module replacement (HMR).</p>
  <Suspense>
    <template #default>
      <Pokemon :pokeIndex="count" />
    </template>
    <template #fallback>
      loading...
    </template>
  </Suspense>
  <p>
    <span>Count is: {{ count }}</span>
  </p>
  <button @click="crement(1)">increment</button>
  <button @click="crement(-1)">decrement</button>
</template>

<script lang="ts">
import Pokemon from "./components/Pokemon.vue";

export default {
  components: { Pokemon },
  data: () => ({ count: 1 }),
  methods: {
    crement(val) {
      this.count = Math.max(0, this.count + val);
    },
  },
};
</script>

<style scoped>
h1 {
  color: #4fc08d;
}

h1,
p {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
