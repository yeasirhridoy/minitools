<script setup>
import {useToast} from "primevue/usetoast";

useSeoMeta({
  title: 'Morse Code Converter',
  ogTitle: 'Morse Code Converter',
  description: 'Morse Code Converter',
  ogDescription: 'Morse Code Converter',
  ogImage: '',
})

const toast = useToast();
const mode = ref('text')
const text = ref('')
const code = ref('')
const textToMorse = {
  A: ".-",
  B: "-...",
  C: "-.-.",
  D: "-..",
  E: ".",
  F: "..-.",
  G: "--.",
  H: "....",
  I: "..",
  J: ".---",
  K: "-.-",
  L: ".-..",
  M: "--",
  N: "-.",
  O: "---",
  P: ".--.",
  Q: "--.-",
  R: ".-.",
  S: "...",
  T: "-",
  U: "..-",
  V: "...-",
  W: ".--",
  X: "-..-",
  Y: "-.--",
  Z: "--..",
  0: "-----",
  1: ".----",
  2: "..---",
  3: "...--",
  4: "....-",
  5: ".....",
  6: "-....",
  7: "--...",
  8: "---..",
  9: "----.",
  ".": ".-.-.-",
  ",": "--..--",
  "?": "..--..",
  "'": ".----.",
  "/": "-..-.",
  "(": "-.--.",
  ")": "-.--.-",
  "&": ".-...",
  ":": "---...",
  ";": "-.-.-.",
  "=": "-...-",
  "+": ".-.-.",
  "-": "-....-",
  _: "..--.-",
  '"': ".-..-.",
  $: "...-..-",
  "!": "-.-.--",
  "@": ".--.-.",
  " ": " ",
};
const convertToMorseCode = () => {
  const inputText = text.value.toUpperCase();
  const morseArray = inputText.split("").map((char) => {
    if (char === " ") {
      return " ";
    } else if (textToMorse[char]) {
      return textToMorse[char];
    }
    return "";
  });

  code.value = morseArray.join(" ");
};

const convertToText = () => {
  const inputCode = code.value;
  const morseToText = Object.fromEntries(
      Object.entries(textToMorse).map(([key, value]) => [value, key])
  );
  const textArray = inputCode.split(" ").map((char) => {
    if (char === " ") {
      return " ";
    } else if (morseToText[char]) {
      return morseToText[char];
    }
    return "";
  });

  text.value = textArray.join("");
};

const toggleMode = () => {
  mode.value = mode.value === "text" ? "code" : "text";
};

watch(text, () => {
  if (mode.value === 'text') {
    convertToMorseCode();
  }
});
watch(code, () => {
  if (mode.value === 'code') {
    convertToText();
  }
});

const copyToClipboard = () => {
  const value = mode.value === 'text' ? code.value : text.value;
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
        <h1>Morse Code Converter
          <Button @click="toggleMode" v-tooltip="mode === 'text' ? 'Convert code to text' : 'Convert text to code'"
                  type="button" icon="pi pi-arrow-right-arrow-left"/>
        </h1>
        <p>{{ mode === 'text' ? 'Converts text to Morse code.' : 'Converts Morse code to text.' }}</p>
        <template v-if="mode==='text'">
          <Textarea v-model="text" auto-resize autofocus rows="10" class="w-full"
                    placeholder="Start typing, or copy and paste your text here..."/>
          <div class="flex justify-content-between mt-4">
            <h4>Output</h4>
            <Button @click="copyToClipboard" size="small" icon="pi pi-copy"/>
          </div>
          <div class="mt-2 border-1 border-round border-gray-300 p-2" style="min-height: 64px">
            {{ code }}
          </div>
        </template>
        <template v-else>
          <Textarea v-model="code" auto-resize autofocus rows="10" class="w-full"
                    placeholder="Start typing, or copy and paste your Morse code here..."/>
          <div class="flex justify-content-between mt-4">
            <h4>Output</h4>
            <Button @click="copyToClipboard" size="small" icon="pi pi-copy"/>
          </div>
          <div class="mt-2 border-1 border-round border-gray-300 p-2" style="min-height: 64px">
            {{ text }}
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>