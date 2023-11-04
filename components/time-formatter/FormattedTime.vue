<script setup>
import {useToast} from "primevue/usetoast";

defineProps({
  time: [String, Number],
});
const toast = useToast();
const copyToClipboard = (value) => {
  navigator.clipboard.writeText(value)
      .then(() => {
        console.log('Text copied to clipboard successfully');
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
  <div>
    <Toast/>
    <div class="p-1 flex justify-content-between align-items-center hover:bg-primary-50">
      <div>{{ time }}</div>
      <Button size="small" icon="pi pi-copy" severity="info" @click="copyToClipboard(time)"/>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>