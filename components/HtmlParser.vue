<script setup>
defineProps({
  text: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <div v-html="text"></div>
</template>

<style scoped lang="scss">

</style>