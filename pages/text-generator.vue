<script setup lang="ts">
const text = ref('')
const paragraphs = ref(1)
const words = ref(100)

const randomPunctuation = () => {
  const punctuation = ['.', ',', '!', '?', ';', ':', '…'];
  return punctuation[Math.floor(Math.random() * punctuation.length)];
}

const generateLoremIpsum = () => {
  const loremIpsumWords = [
    'lorem', 'ipsum', 'dolor', 'sit', 'amet', 'consectetur', 'adipiscing', 'elit', 'sed', 'do', 'eiusmod', 'tempor', 'incididunt', 'ut', 'labore', 'et', 'dolore', 'magna', 'aliqua', 'enim', 'ad', 'minim', 'veniam', 'quis', 'nostrud', 'exercitation', 'ullamco', 'laboris', 'nisi', 'aliquip', 'ex', 'ea', 'commodo', 'consequat', 'duis', 'aute', 'irure', 'in', 'reprehenderit', 'voluptate', 'velit', 'esse', 'cillum', 'eu', 'fugiat', 'nulla', 'pariatur', 'excepteur', 'sint', 'occaecat', 'cupidatat', 'non', 'proident', 'sunt', 'culpa', 'qui', 'officia', 'deserunt', 'mollit', 'anim', 'id', 'est', 'laborum', 'perspiciatis', 'unde', 'omnis', 'iste', 'natus', 'error', 'voluptatem', 'accusantium', 'doloremque', 'laudantium', 'totam', 'rem', 'aperiam', 'eaque', 'ipsa', 'quae', 'ab', 'illo', 'inventore', 'veritatis', 'quasi', 'architecto', 'beatae', 'vitae', 'dicta', 'explicabo', 'nemo', 'ipsam', 'voluptas', 'aspernatur', 'aut', 'odit', 'consequuntur', 'magni', 'ratione', 'sequi', 'nesciunt', 'neque', 'porro', 'quisquam', 'est', 'adipisci', 'velit', 'numquam', 'eius', 'modi', 'tempora', 'magnam', 'aliquam', 'quaerat', 'eniam', 'nostrum', 'exercitationem', 'ullam', 'corporis', 'suscipit', 'laboriosam', 'aliquid', 'consequatur', 'autem', 'vel', 'eum', 'iure', 'quam', 'nihil', 'molestiae', 'illum', 'quo', 'at', 'vero', 'eos', 'accusamus', 'iusto', 'odio', 'dignissimos', 'ducimus', 'blanditiis', 'praesentium', 'voluptatum', 'deleniti', 'atque'
  ];

  let loremIpsumText = '';
  for (let p = 0; p < paragraphs.value; p++) {
    for (let w = 0; w < words.value; w++) {
      const randomWord = loremIpsumWords[Math.floor(Math.random() * loremIpsumWords.length)];
      loremIpsumText += randomWord + ' ';

      if (w === words.value - 1) {
        loremIpsumText = loremIpsumText.slice(0, -1);
        loremIpsumText += '.';
      } else if (Math.random() > 0.9) {
        loremIpsumText = loremIpsumText.slice(0, -1);
        loremIpsumText += randomPunctuation() + ' ';
      }
    }
    loremIpsumText += '\n\n';
  }

  loremIpsumText = loremIpsumText.replace(/(^\s*\w|[\.\!\?]\s*\w)/g, (c) => c.toUpperCase())

  text.value = loremIpsumText.trim();
}

</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Text Generator</h1>
        <p>Generate random text for your designs.</p>
        <div class="flex flex-wrap gap-2 p-fluid">
          <div class="flex-auto">
            <label for="paragraph" class="font-bold block mb-2">Number of paragraph</label>
            <InputNumber id="paragraph" class="flex-1" v-model="paragraphs" :min="1" :max="100"/>
          </div>
          <div class="flex-auto">
            <label for="word" class="font-bold block mb-2">Number of words</label>
            <InputNumber id="word" class="flex-1" v-model="words" :min="1" :max="1000"/>
          </div>
          <Button class="flex-auto" @click="generateLoremIpsum()" label="Generate"/>
          <SinglePreviewBox :text="text"/>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>