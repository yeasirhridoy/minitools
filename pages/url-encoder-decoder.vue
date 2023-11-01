<script setup>
import {useToast} from "primevue/usetoast";

const toast = useToast();
const url = ref('');
const operation = ref('encode'); // Default to URL encoding
const result = ref('');

const processURL = () => {
  if (operation.value === 'encode') {
    result.value = encodeURIComponent(url.value);
  } else {
    result.value = decodeURIComponent(url.value);
  }
};

watch([url, operation], processURL);

const copyToClipboard = () => {
  const value = result.value
  navigator.clipboard.writeText(value)
      .then(() => {
        console.log('Copied to clipboard successfully');
        toast.add({
          severity: 'success',
          summary: 'Copied to clipboard',
          detail: value,
          life: 3000
        });
      })
      .catch((err) => {
        console.error('Copy to clipboard failed:', err);
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
        <h1>URL Encoder Decoder</h1>
        <div class="flex flex-wrap gap-3 mb-2">
          <div class="flex align-items-center">
            <RadioButton v-model="operation" inputId="encode" name="encode" value="encode"/>
            <label for="encode" class="ml-2">Encode</label>
          </div>
          <div class="flex align-items-center">
            <RadioButton v-model="operation" inputId="decode" name="decode" value="decode"/>
            <label for="decode" class="ml-2">Decode</label>
          </div>
        </div>
        <InputText v-model="url" placeholder="Enter URL" class="w-full"/>
        <div class="flex justify-content-between mt-2">
          <h4>Output</h4>
          <Button @click="copyToClipboard" size="small" icon="pi pi-copy"/>
        </div>
        <div class="mt-2 border-1 border-round border-gray-300 p-2" style="min-height: 64px">
          {{ result }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>