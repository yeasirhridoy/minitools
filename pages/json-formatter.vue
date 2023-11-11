<script setup>
import {useToast} from "primevue/usetoast";

const inputJson = ref();
const toast = useToast();

const formattedJson = computed(() => {
  if (inputJson.value) {
    try {
      const fixedJsonString = inputJson.value.replace(/(['"])?([a-zA-Z0-9_]+)(['"])?:/g, '"$2":');
      const finalFixedJsonString = fixedJsonString.replace(/'/g, '"');
      return JSON.stringify(JSON.parse(finalFixedJsonString), null, 2);
    } catch (e) {
      return '';
    }
  }
  return '';
});

useSeoMeta({
  title: 'JSON Formatter',
  ogTitle: 'JSON Formatter',
  description: 'JSON Formatter',
  ogDescription: 'JSON Formatter',
  ogImage: '',
})

const copyToClipboard = () => {
  navigator.clipboard.writeText(formattedJson.value)
      .then(() => {
        toast.add({
          severity: 'success',
          summary: 'Copied to clipboard',
          life: 3000
        });
      })
      .catch((err) => {
        toast.add({
          severity: 'error',
          summary: 'Copy to clipboard failed',
          life: 3000
        });
      });
};
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <Toast/>
        <h1>JSON Formatter</h1>
        <p>Format JSON data.</p>
        <Textarea v-model="inputJson" autofocus rows="10" class="w-full"
                  placeholder="Start typing, or copy and paste your json here..."/>
        <div class="mt-4">
          <h4>Output</h4>
          <Textarea v-model="formattedJson" rows="10" class="w-full"
                    :placeholder="inputJson && !formattedJson ? 'Invalid JSON': 'Formatted JSON output'"/>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>