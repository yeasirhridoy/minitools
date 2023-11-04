<script setup>
const text = ref('')
const paragraphs = ref(2)
const words = ref(100)

const generateLoremIpsum = () => {
  const loremIpsumWords = [
    'Lorem', 'ipsum', 'dolor', 'sit', 'amet', 'consectetur', 'adipiscing', 'elit', 'sed', 'do', 'eiusmod',
    'tempor', 'incididunt', 'ut', 'labore', 'et', 'dolore', 'magna', 'aliqua', 'Ut', 'enim', 'ad', 'minim',
    'veniam', 'quis', 'nostrud', 'exercitation', 'ullamco', 'laboris', 'nisi', 'ut', 'aliquip', 'ex', 'ea',
    'commodo', 'consequat', 'Duis', 'aute', 'irure', 'dolor', 'in', 'reprehenderit', 'in', 'voluptate', 'velit',
    'esse', 'cillum', 'dolore', 'eu', 'fugiat', 'nulla', 'pariatur', 'Excepteur', 'sint', 'occaecat', 'cupidatat',
    'non', 'proident', 'sunt', 'in', 'culpa', 'qui', 'officia', 'deserunt', 'mollit', 'anim', 'id', 'est', 'laborum'
  ];

  let loremIpsumText = '';
  for (let p = 0; p < paragraphs.value; p++) {
    for (let w = 0; w < words.value; w++) {
      const randomWord = loremIpsumWords[Math.floor(Math.random() * loremIpsumWords.length)];
      loremIpsumText += randomWord + ' ';
    }
    loremIpsumText += '\n\n'; // Add a double newline to separate paragraphs
  }

  text.value = loremIpsumText.trim(); // Remove trailing whitespace
}

</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Text Generator</h1>
        <p>Generate random text for your designs.</p>
        <Button @click="generateLoremIpsum()" label="Generate"/>
        <div>
          {{ text}}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>