<script lang="ts" setup>
import {ref, watch} from "vue";
import type Fuse from "fuse.js";

type Result = Fuse.FuseResult<string>[]

const names = ['Tim', 'Joe', 'Bel', 'Max', 'Lee']
const text = ref('')
const results = ref<Result>([])

watch(text, async value => {
  const Fuse = (await import('fuse.js')).default
  const fuse = new Fuse(names)

  results.value = fuse.search(value)
})
</script>

<template>
<div>
  <input v-model="text" placeholder="Search" type="text" >
  <pre>{{ results }}</pre>
</div>
</template>

<style>
#app {
  color: #2c3e50;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  margin-top: 60px;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
