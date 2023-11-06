<script setup>
const text = ref('')
const regex = ref('')

const outputText = computed(() => {
  try {
    const re = new RegExp(regex.value, 'g')
    return text.value.replace(re, (match) => {
      return `<span class="bg-yellow-200">${match}</span>`
    })
  } catch (e) {
    return text.value
  }
})
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Regex Checker</h1>
        <p>Match a string against a regular expression.</p>
        <div class="grid gap-2">
          <div class="col-12">
            <div class="flex-auto">
              <label for="regex" class="font-bold mb-2">Regular Expression</label>
              <InputText id="regex" v-model="regex" class="w-full mt-2" placeholder="Enter a regular expression"/>
            </div>
          </div>
          <div class="col-12">
            <div class="flex-auto">
              <label for="text" class="font-bold mb-2">Text</label>
              <Textarea id="text" v-model="text" auto-resize autofocus rows="10" class="w-full mt-2"
                        placeholder="Enter text to match against the regular expression"/>
            </div>
          </div>
          <div class="col-12">
            <h4>Output</h4>
            <div class="mt-2 border-1 border-round border-gray-300 p-2 overflow-auto"
                 style="min-height: 64px;white-space:pre-wrap;">
              <HtmlParser :text="outputText"/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>