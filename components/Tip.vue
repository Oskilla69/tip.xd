<template>
  <div class="tip-container">
    <h1>{{ tip }}</h1>
  </div>
</template>

<script setup lang="ts">
interface Props {
  tip: string;
}
const props = defineProps<Props>();
</script>

<style scoped>
.tip-container {
  background-color: #006afe;
  color: white;
  padding: 5px;
  text-align: center;
  align-items: center;
  justify-content: center;
  display: flex;
  cursor: pointer;
}
</style>
