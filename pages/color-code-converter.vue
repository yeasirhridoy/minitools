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
const convertColorCodes = (type: string) => {
  switch (type) {
    case 'hex':
      convertHex()
      break
    case 'rgb':
      convertRgb()
      break
    case 'hsl':
      convertHsl()
      break
    case 'cmyk':
      convertCmyk()
      break
  }
};

const convertHex = () => {
  const hexValue = hex.value.trim();

  if (hexValue.length !== 6) {
    console.error('Invalid HEX format');
    return;
  }

  // Convert to RGB
  const [r, g, b] = [
    parseInt(hexValue.slice(0, 2), 16),
    parseInt(hexValue.slice(2, 4), 16),
    parseInt(hexValue.slice(4, 6), 16)
  ];

  rgb.value = `${r},${g},${b}`;

  // Convert to HSL
  const r1 = r / 255;
  const g1 = g / 255;
  const b1 = b / 255;
  const max = Math.max(r1, g1, b1);
  const min = Math.min(r1, g1, b1);
  let h = 0;
  let s = 0;
  let l = (max + min) / 2;

  if (max !== min) {
    const d = max - min;
    s = l > 0.5 ? d / (2 - max - min) : d / (max + min);

    switch (max) {
      case r1:
        h = (g1 - b1) / d + (g1 < b1 ? 6 : 0);
        break;
      case g1:
        h = (b1 - r1) / d + 2;
        break;
      case b1:
        h = (r1 - g1) / d + 4;
        break;
    }

    h /= 6;
  }

  hsl.value = `${Math.round(h * 360)},${Math.round(s * 100)}%,${Math.round(l * 100)}%`;

  // Convert to CMYK
  const r2 = r / 255;
  const g2 = g / 255;
  const b2 = b / 255;
  const k = 1 - Math.max(r2, g2, b2);
  const c = (1 - r2 - k) / (1 - k);
  const m = (1 - g2 - k) / (1 - k);
  const y = (1 - b2 - k) / (1 - k);

  cmyk.value = `${Math.round(c * 100)}%,${Math.round(m * 100)}%,${Math.round(y * 100)}%,${Math.round(k * 100)}%`;
};

const convertRgb = () => {
  const rgbRegex = /^(\d{1,3}),\s*(\d{1,3}),\s*(\d{1,3})$/;
  const match = rgb.value.match(rgbRegex);

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
const convertHsl = () => {

};
const convertCmyk = () => {

};
</script>

<template>
  <div class="grid">
    <Toast/>
    <div class="col-12">
      <div class="card">
        <h1>Color Code Converter</h1>
        <p>Converts color codes between RGB, HEX, HSL, and CMYK</p>
        <div class="flex flex-column gap-3 max-w-fit">
          <div class="p-inputgroup flex-1 w-full">
            <ColorPicker v-model="hex" class="hidden" :style="{backgroundColor: `#${hex}`}" ref="colorPicker"/>
            <div class="w-full h-2rem" :style="{backgroundColor: `#${hex}`}"></div>
          </div>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">
              HEX
            </span>
            <InputText type="text" v-model="hex" placeholder="000000"/>
            <Button severity="success" @click="convertColorCodes('hex')">Convert</Button>
            <Button icon="pi pi-copy" severity="info" @click="copyToClipboard(hex)"/>
          </div>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">RGB</span>
            <InputText type="text" v-model="rgb" placeholder="R,G,B"/>
            <Button severity="success" @click="convertColorCodes('rgb')">Convert</Button>
            <Button icon="pi pi-copy" severity="info" @click="copyToClipboard(rgb)"/>
          </div>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">HSL</span>
            <InputText type="text" v-model="hsl" placeholder="H,S,L"/>
            <Button severity="success" @click="convertColorCodes('hsl')">Convert</Button>
            <Button icon="pi pi-copy" severity="info" @click="copyToClipboard(hsl)"/>
          </div>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">CMYK</span>
            <InputText type="text" v-model="cmyk" placeholder="C,M,Y,K"/>
            <Button severity="success" @click="convertColorCodes('cmyk')">Convert</Button>
            <Button icon="pi pi-copy" severity="info" @click="copyToClipboard(cmyk)"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>