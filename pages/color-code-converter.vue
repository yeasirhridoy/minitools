<script setup lang="ts">
import {useToast} from "primevue/usetoast";

const toast = useToast();
const color = ref('#000000')
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

const toRgb = (hexValue) => {
  if (hexValue.length === 3) {
    hexValue = hexValue.split('').map((value) => value + value).join('');
  }
  color.value = hexValue;
  const [r, g, b] = [
    parseInt(hexValue.slice(0, 2), 16),
    parseInt(hexValue.slice(2, 4), 16),
    parseInt(hexValue.slice(4, 6), 16)
  ];

  rgb.value = `${r},${g},${b}`;
}
const toHsl = (hexValue) => {
  if (hexValue.length === 3) {
    hexValue = hexValue.split('').map((value) => value + value).join('');
  }
  color.value = hexValue;
  const [r, g, b] = [
    parseInt(hexValue.slice(0, 2), 16),
    parseInt(hexValue.slice(2, 4), 16),
    parseInt(hexValue.slice(4, 6), 16)
  ];
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
}
const toCmyk = (hexValue) => {
  if (hexValue.length === 3) {
    hexValue = hexValue.split('').map((value) => value + value).join('');
  }
  color.value = hexValue;
  const [r, g, b] = [
    parseInt(hexValue.slice(0, 2), 16),
    parseInt(hexValue.slice(2, 4), 16),
    parseInt(hexValue.slice(4, 6), 16)
  ];
  const r2 = r / 255;
  const g2 = g / 255;
  const b2 = b / 255;
  const k = 1 - Math.max(r2, g2, b2);
  const c = (1 - r2 - k) / (1 - k);
  const m = (1 - g2 - k) / (1 - k);
  const y = (1 - b2 - k) / (1 - k);

  cmyk.value = `${Math.round(c * 100)}%,${Math.round(m * 100)}%,${Math.round(y * 100)}%,${Math.round(k * 100)}%`;
}
const convertHex = () => {
  if (!isValidHex.value || hex.value === '') {
    return;
  }
  if (hex.value.startsWith('#')) {
    hex.value = hex.value.slice(1);
  }
  const hexValue = hex.value.trim();
  toRgb(hexValue);
  toHsl(hexValue);
  toCmyk(hexValue)
};
const convertRgb = () => {
  if (!isValidRgb.value || rgb.value === '') {
    return;
  }
  const [r, g, b] = rgb.value.split(',').map((value) => parseInt(value.trim(), 10));
  hex.value = [r, g, b].map((value) => {
    const hex = value.toString(16);
    return hex.length === 1 ? `0${hex}` : hex;
  }).join('');
  toHsl(hex.value);
  toCmyk(hex.value);
};
const convertHsl = () => {
  if (!isValidHsl.value || hsl.value === '') {
    return;
  }
  const [h, s, l] = hsl.value.split(',').map((value) => parseInt(value.trim(), 10));
  const h1 = h / 360;
  const s1 = s / 100;
  const l1 = l / 100;
  let r1;
  let g1;
  let b1;

  if (s1 === 0) {
    r1 = g1 = b1 = l1;
  } else {
    const hue2rgb = (p, q, t) => {
      if (t < 0) {
        t += 1;
      }
      if (t > 1) {
        t -= 1;
      }
      if (t < 1 / 6) {
        return p + (q - p) * 6 * t;
      }
      if (t < 1 / 2) {
        return q;
      }
      if (t < 2 / 3) {
        return p + (q - p) * (2 / 3 - t) * 6;
      }
      return p;
    };
    const q = l1 < 0.5 ? l1 * (1 + s1) : l1 + s1 - l1 * s1;
    const p = 2 * l1 - q;
    r1 = hue2rgb(p, q, h1 + 1 / 3);
    g1 = hue2rgb(p, q, h1);
    b1 = hue2rgb(p, q, h1 - 1 / 3);
  }
  const r = Math.round(r1 * 255);
  const g = Math.round(g1 * 255);
  const b = Math.round(b1 * 255);
  hex.value = [r, g, b].map((value) => {
    const hex = value.toString(16);
    return hex.length === 1 ? `0${hex}` : hex;
  }).join('');
  toRgb(hex.value);
  toCmyk(hex.value);
};
const convertCmyk = () => {
  if (!isValidCmyk.value || cmyk.value === '') {
    return;
  }
  const [c, m, y, k] = cmyk.value.split(',').map((value) => parseInt(value.trim(), 10));
  const r = 255 * (1 - c / 100) * (1 - k / 100);
  const g = 255 * (1 - m / 100) * (1 - k / 100);
  const b = 255 * (1 - y / 100) * (1 - k / 100);
  hex.value = [r, g, b].map((value) => {
    const hex = value.toString(16);
    return hex.length === 1 ? `0${hex}` : hex;
  }).join('');
  toRgb(hex.value);
  toHsl(hex.value);
};

const isValidColor = (colorValue, regex) => {
  if (colorValue === '') {
    return true;
  }
  const match = colorValue.match(regex);
  if (!match) {
    return false;
  }
  if (regex === /^(\d{1,3}),\s*(\d{1,3}),\s*(\d{1,3})$/) {
    return match.slice(1).every((component, index) => {
      const c = parseInt(component, 10);
      return !isNaN(c) && c >= 0 && c <= 255;
    });
  }
  if (regex === /^(\d{1,3}),\s*(\d{1,3})%,\s*(\d{1,3})%$/) {
    return match.slice(1).every((component, index) => {
      const c = parseInt(component, 10);
      return !isNaN(c) && c >= 0 && c <= 100;
    });
  }
  if (regex === /^(\d{1,3})%,\s*(\d{1,3})%,\s*(\d{1,3})%,\s*(\d{1,3})%$/) {
    return match.slice(1).every((component, index) => {
      const c = parseInt(component, 10);
      return !isNaN(c) && c >= 0 && c <= 100;
    });
  }
  return true;
};

const isValidHex = computed(() => isValidColor(hex.value, /^#?([0-9a-fA-F]{3}|[0-9a-fA-F]{6})$/));
const isValidRgb = computed(() => isValidColor(rgb.value, /^(\d{1,3}),\s*(\d{1,3}),\s*(\d{1,3})$/));
const isValidHsl = computed(() => isValidColor(hsl.value, /^(\d{1,3}),\s*(\d{1,3})%,\s*(\d{1,3})%$/));
const isValidCmyk = computed(() => isValidColor(cmyk.value, /^(\d{1,3})%,\s*(\d{1,3})%,\s*(\d{1,3})%,\s*(\d{1,3})%$/));

watch(() => color.value, (value) => {
  hex.value = value;
  convertColorCodes('hex');
});
</script>

<template>
  <div class="grid">
    <Toast/>
    <div class="col-12">
      <div class="card">
        <h1>Color Code Converter</h1>
        <p>Converts color codes between RGB, HEX, HSL, and CMYK</p>
        <div class="flex flex-column gap-3 max-w-fit">
          <ColorPicker v-model="color" :pt="{
              input: {
                class: 'w-full h-full'
              }
            }"/>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">
              HEX
            </span>
            <InputText type="text" v-model="hex" :value="hex" placeholder="000000" :class="{'p-invalid': !isValidHex}"/>
            <Button severity="success" @click="convertColorCodes('hex')">Convert</Button>
            <Button icon="pi pi-copy" severity="info" @click="copyToClipboard(hex)"/>
          </div>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">RGB</span>
            <InputText type="text" v-model="rgb" placeholder="R,G,B" :class="{'p-invalid':!isValidRgb}"/>
            <Button severity="success" @click="convertColorCodes('rgb')">Convert</Button>
            <Button icon="pi pi-copy" severity="info" @click="copyToClipboard(rgb)"/>
          </div>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">HSL</span>
            <InputText type="text" v-model="hsl" placeholder="H,S,L" :class="{'p-invalid':!isValidHsl}"/>
            <Button severity="success" @click="convertColorCodes('hsl')">Convert</Button>
            <Button icon="pi pi-copy" severity="info" @click="copyToClipboard(hsl)"/>
          </div>
          <div class="p-inputgroup flex-1">
            <span class="p-inputgroup-addon w-1">CMYK</span>
            <InputText type="text" v-model="cmyk" placeholder="C,M,Y,K" :class="{'p-invalid':!isValidCmyk}"/>
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