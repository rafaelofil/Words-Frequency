<script setup lang="ts">
import BoxWord from './components/BoxWord.vue';
</script>

<template>
  <h1 class="title">Word Frequency</h1>

  <div >
    <BoxWord />
  </div>
</template>

<style>
@import './assets/base.css';

body {
  background: var(--vt-c-white);
}

.title {
  width: 100%;
  margin-top: 10rem;
  font-size: 3rem;

  display: flex;
  justify-content: center;
}

</style>
