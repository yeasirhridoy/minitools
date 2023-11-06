<script setup>
import {diff_match_patch} from 'diff-match-patch';
const textToCompare = ref('')
const textToCompareWith = ref('')

const output = computed(() => {
  const dmp = new diff_match_patch()
  const diff = dmp.diff_main(textToCompare.value, textToCompareWith.value)
  dmp.diff_cleanupSemantic(diff)
  return dmp.diff_prettyHtml(diff)
})

</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Text Comparator</h1>
        <p>Compare two texts and see the differences.</p>
        <div class="grid">
          <div class="col-12 md:col-6">
            <div class="flex-auto">
              <label for="textToCompareWith" class="font-bold mb-2">Text to compare with</label>
              <Textarea id="textToCompareWith" v-model="textToCompareWith" auto-resize autofocus rows="10"
                        class="w-full mt-2" placeholder="Enter text to compare with"/>
            </div>
          </div>
          <div class="col-12 md:col-6">
            <div class="flex-auto">
              <label for="textToCompare" class="font-bold mb-2">Text to compare</label>
              <Textarea id="textToCompare" v-model="textToCompare" auto-resize autofocus rows="10" class="w-full mt-2"
                        placeholder="Enter text to compare"/>
            </div>
          </div>
          <div class="col-12">
            <h4>Output</h4>
            <div class="mt-2 border-1 border-round border-gray-300 p-2 overflow-auto"
                 style="min-height: 64px;white-space:pre-wrap;">
              <HtmlParser :text="output"/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>