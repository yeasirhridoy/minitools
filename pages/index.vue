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
    title: 'Age Calculator',
    to: '/age-calculator'
  },
  {
    title: 'Text Generator',
    to: '/text-generator'
  },
  {
    title: 'Unit Converter',
    to: '/unit-converter'
  },
  {
    title: 'Password Generator',
    to: '/password-generator'
  },
  {
    title: 'Case Converter',
    to: '/case-converter'
  },
  {
    title: 'Regex Checker',
    to: '/regex-checker'
  },
  {
    title: 'Text Comparator',
    to: '/text-comparator'
  }
]

useSeoMeta({
  title: 'Home',
  ogTitle: 'Home',
  description: 'Home page of Online Tools powered by Brilliant Softs',
  ogDescription: 'Home page of Online Tools powered by Brilliant Softs',
  ogImage: '',
  twitterCard: 'summary_large_image',
})
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
