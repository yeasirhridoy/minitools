<script setup lang="ts">
import {useToast} from "primevue/usetoast";

const outputCase = ref('lowercase')
const text = ref('')

const toast = useToast();
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
      return text.value.toLowerCase().replace(/(^\s*\w|[\.\!\?]\s*\w)/g, (c) => c.toUpperCase())
    default:
      return text.value
  }
})

const copyToClipboard = () => {
  const value = outputText.value as string
  navigator.clipboard.writeText(value)
      .then(() => {
        toast.add({
          severity: 'success',
          summary: 'Copied to clipboard',
          detail: value,
          life: 3000
        });
      })
      .catch((err) => {
        toast.add({
          severity: 'error',
          summary: 'Copy to clipboard failed',
          detail: err,
          life: 3000
        });
      });
};
</script>

<template>
  <div class="grid">
    <Toast/>
    <div class="col-12">
      <div class="card">
        <h1>Case Converter</h1>
        <div class="flex flex-wrap gap-3 mb-2">
          <div v-for="(item,i) in cases" class="flex align-items-center">
            <RadioButton :id="item" v-model="outputCase" :value="item"/>
            <label :for="item" class="ml-2">{{ item.toUpperCase() }}</label>
          </div>
        </div>
        <Textarea v-model="text" auto-resize autofocus rows="10" class="w-full mt-2"
                  placeholder="Start typing, or copy and paste your text here..."/>
        <div class="flex justify-content-between mt-4">
          <h4>Output</h4>
          <Button @click="copyToClipboard" size="small" icon="pi pi-copy"/>
        </div>
        <div class="mt-2 border-1 border-round border-gray-300 p-2" style="min-height: 64px">
          {{ outputText }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>