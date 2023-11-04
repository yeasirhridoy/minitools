<script setup lang="ts">
const items = [
  {
    title: 'Word Counter',
    to: '/word-counter'
  },
  {
    title: 'Color Code Converter',
    to: '/color-code-converter'
  },
  {
    title: 'Morse Code Converter',
    to: '/morse-code-converter'
  },
  {
    title: 'URL Encoder Decoder',
    to: '/url-encoder-decoder'
  },
  {
    title: 'Time Formatter',
    to: '/time-formatter'
  },
  {
    title: 'Birthday Calculator',
    to: '/birthday-calculator'
  }
]
</script>

<template>
  <div class="grid">
    <div v-for="(item,i) in items" :key="i" class="col-12 lg:col-6 xl:col-3">
      <div class="card mb-0">
        <NuxtLink :to="item.to">{{ item.title }}</NuxtLink>
      </div>
    </div>
  </div>
</template>
