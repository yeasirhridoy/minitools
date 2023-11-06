<script setup>
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
        <div class="flex-auto">
          <label for="url" class="font-bold">URL</label>
          <InputText v-model="url" placeholder="Enter URL" class="w-full mt-2"/>
        </div>
        <SinglePreviewBox :text="result"/>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>