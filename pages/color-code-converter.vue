<script setup lang="ts">
import {useToast} from "primevue/usetoast";

const toast = useToast();
const hex = ref('')
const rgb = ref('')
const hsl = ref('')
const cmyk = ref('')

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


const updateColorCodes = () => {
  const hexValue = hex.value.trim();
  const rgbValue = rgb.value.trim();
  const hslValue = hsl.value.trim();
  const cmykValue = cmyk.value.trim();

  if (hexValue) {
    const rgbColor = hexToRgb(hexValue);
    if (rgbColor) {
      rgb.value = rgbColor;
    }
  } else if (rgbValue) {
    // RGB to HEX conversion
    const hexColor = rgbToHex(rgbValue);
    if (hexColor) {
      hex.value = hexColor;
    }
  } else if (hslValue) {
    // HSL to RGB conversion
    const rgbColor = hslToRgb(hslValue);
    if (rgbColor) {
      rgb.value = rgbColor;
    }
  } else if (cmykValue) {
    // CMYK to RGB conversion
    const rgbColor = cmykToRgb(cmykValue);
    if (rgbColor) {
      rgb.value = rgbColor;
    }
  }
};

const hexToRgb = (hex) => {
  hex = hex.replace('#', '');
  if (hex.length !== 6) {
    return null;
  }
  const values = hex.split('');
  const r = parseInt(values[0].toString() + values[1].toString(), 16);
  const g = parseInt(values[2].toString() + values[3].toString(), 16);
  const b = parseInt(values[4].toString() + values[5].toString(), 16);
  return `${r},${g},${b}`;
};

const rgbToHex = (rgb) => {
  const rgbRegex = /^(\d{1,3}),\s*(\d{1,3}),\s*(\d{1,3})$/;
  const match = rgb.match(rgbRegex);

  if (!match) {
    return '';
  }

  const r = parseInt(match[1], 10);
  const g = parseInt(match[2], 10);
  const b = parseInt(match[3], 10);

  if (isNaN(r) || isNaN(g) || isNaN(b) || r < 0 || r > 255 || g < 0 || g > 255 || b < 0 || b > 255) {
    return '';
  }

  const toHex = (c) => {
    const hex = c.toString(16);
    return hex.length === 1 ? '0' + hex : hex;
  };

  return `#${toHex(r)}${toHex(g)}${toHex(b)}`;
};

const hslToRgb = (hsl) => {
  // Implement HSL to RGB conversion logic here
};

const cmykToRgb = (cmyk) => {
  // Implement CMYK to RGB conversion logic here
};

watch([hex, rgb, hsl, cmyk], updateColorCodes);

onMounted(() => {
  // You can add any additional setup code here
});
</script>

<template>
  <div class="grid">
    <Toast/>
    <div class="col-12">
      <div class="card">
        <h1>Color Code Converter</h1>
        <p>Converts color codes between RGB, HEX, HSL, and CMYK</p>
        <div class="flex flex-column gap-3">
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">
              HEX
            </span>
            <InputText type="text" v-model="hex" placeholder="000000"/>
            <Button icon="pi pi-copy" severity="success" @click="copyToClipboard(hex)"/>
          </div>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">RGB</span>
            <InputText type="text" v-model="rgb" placeholder="R,G,B"/>
            <Button icon="pi pi-copy" severity="success" @click="copyToClipboard(rgb)"/>
          </div>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">HSL</span>
            <InputText type="text" v-model="hsl" placeholder="H,S,L"/>
            <Button icon="pi pi-copy" severity="success" @click="copyToClipboard(hsl)"/>
          </div>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">CMYK</span>
            <InputText type="text" v-model="cmyk" placeholder="C,M,Y,K"/>
            <Button icon="pi pi-copy" severity="success" @click="copyToClipboard(cmyk)"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>