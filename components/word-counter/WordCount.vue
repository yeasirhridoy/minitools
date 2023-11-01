<script setup lang="ts">
defineProps({
  title: String,
  value: Number
});
</script>

<template>
  <div class="flex gap-2 text-lg md:text-xl">
    <div class="card-header">{{ title }}:</div>
    <div class="card-body">{{ value }}</div>
  </div>
</template>

<style scoped lang="scss">

</style>