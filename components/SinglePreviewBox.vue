<script setup lang="ts">
import {useToast} from "primevue/usetoast";

const props = defineProps({
  text: {
    required: true
  }
})

const toast = useToast();
const copyToClipboard = () => {
  const value = props.text
  navigator.clipboard.writeText(value)
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
  <div class="flex-auto" v-bind="$attrs">
    <Toast/>
    <div class="flex justify-content-between mt-4">
      <h4>Output</h4>
      <Button @click="copyToClipboard" size="small" icon="pi pi-copy"/>
    </div>
    <div class="mt-2 border-1 border-round border-gray-300 p-2 overflow-auto" style="min-height: 64px;white-space:pre-wrap;">
      {{ text }}
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>