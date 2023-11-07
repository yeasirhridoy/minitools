<script setup lang="ts">

useSeoMeta({
  title: 'Case Converter',
  ogTitle: 'Case Converter',
  description: 'Case Converter',
  ogDescription: 'Case Converter',
  ogImage: '',
})

const outputCase = ref('lowercase')
const text = ref('')

const cases = [
  'lowercase',
  'uppercase',
  'titlecase',
  'sentencecase',
]

const outputText = computed(() => {
  switch (outputCase.value) {
    case 'lowercase':
      return text.value.toLowerCase()
    case 'uppercase':
      return text.value.toUpperCase()
    case 'titlecase':
      return text.value.replace(/\w\S*/g, (txt) => {
        return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase()
      })
    case 'sentencecase':
      return text.value.toLowerCase().replace(/(^\s*\w|[.!?]\s*\w)/g, (c) => c.toUpperCase())
    default:
      return text.value
  }
})
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Case Converter</h1>
        <p>Convert text to different cases.</p>
        <div class="flex flex-wrap gap-3 mb-2">
          <div v-for="(item,i) in cases" class="flex align-items-center">
            <RadioButton :id="item" v-model="outputCase" :value="item"/>
            <label :for="item" class="ml-2">{{ item.toUpperCase() }}</label>
          </div>
        </div>
        <Textarea v-model="text" auto-resize autofocus rows="10" class="w-full mt-2"
                  placeholder="Start typing, or copy and paste your text here..."/>
        <SinglePreviewBox :text="outputText"/>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>