<script setup lang="ts">
import { ref } from 'vue';
const count = ref(0);
const status = 6;
const visits = ref([
  { visitStatusStr: 'Cancelled', visitStatus: 6 },
  { visitStatusStr: 'Requested', visitStatus: 1 },
  { visitStatusStr: 'Declined', visitStatus: 4 },
  { visitStatusStr: 'Request Declined', visitStatus: 8 },
]);

let actives = visits.value.filter(
  (v) => v.visitStatus === status || (v.visitStatus === 8 && status === 6)
);
defineProps<{ msg: string }>();
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <div v-for="active in actives">{{ active.visitStatus }}: {{ active.visitStatusStr }}</div>
    <!--p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p-->
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
