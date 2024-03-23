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
  },
  {
    title: 'BMI Calculator',
    to: '/bmi-calculator'
  },
  {
    title: 'Timezone Converter',
    to: '/timezone-converter'
  },
  {
    title: 'JSON Formatter',
    to: '/json-formatter'
  },
  {
    title: 'Math Generator',
    to: '/math-generator'
  },
  // {
  //   title: 'JSON Validator',
  //   to: '/json-validator'
  // },
  // {
  //   title: 'XML Formatter',
  //   to: '/xml-formatter'
  // },
  // {
  //   title: 'XML Validator',
  //   to: '/xml-validator'
  // },
  // {
  //   title: 'HTML Formatter',
  //   to: '/html-formatter'
  // },
  // {
  //   title: 'HTML Validator',
  //   to: '/html-validator'
  // },
  // {
  //   title: 'CSV Formatter',
  //   to: '/csv-formatter'
  // },
  // {
  //   title: 'CSV Validator',
  //   to: '/csv-validator'
  // },
  // {
  //   title: 'YAML Formatter',
  //   to: '/yaml-formatter'
  // },
  // {
  //   title: 'YAML Validator',
  //   to: '/yaml-validator'
  // },
  // {
  //   title: 'SQL Formatter',
  //   to: '/sql-formatter'
  // },
  // {
  //   title: 'SQL Validator',
  //   to: '/sql-validator'
  // },
  // {
  //   title: 'Javascript Formatter',
  //   to: '/javascript-formatter'
  // },
  // {
  //   title: 'Javascript Validator',
  //   to: '/javascript-validator'
  // },
  // {
  //   title: 'CSS Formatter',
  //   to: '/css-formatter'
  // },
  // {
  //   title: 'CSS Validator',
  //   to: '/css-validator'
  // },
  // {
  //   title: 'XML to JSON Converter',
  //   to: '/xml-to-json-converter'
  // },
  // {
  //   title: 'JSON to XML Converter',
  //   to: '/json-to-xml-converter'
  // },
  // {
  //   title: 'XML to CSV Converter',
  //   to: '/xml-to-csv-converter'
  // },
  // {
  //   title: 'CSV to XML Converter',
  //   to: '/csv-to-xml-converter'
  // },
  // {
  //   title: 'XML to YAML Converter',
  //   to: '/xml-to-yaml-converter'
  // },
  // {
  //   title: 'YAML to XML Converter',
  //   to: '/yaml-to-xml-converter'
  // },
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
    <div class="col-12">
      <h1 class="text-center">Online Tools</h1>
    </div>
    <div v-for="(item,i) in items" :key="i" class="col-12 lg:col-6 xl:col-3">
      <div class="card mb-0">
        <NuxtLink :to="item.to">{{ item.title }}</NuxtLink>
      </div>
    </div>
  </div>
</template>
