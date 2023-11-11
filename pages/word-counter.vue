<script setup lang="ts">

import WordCount from "../components/word-counter/WordCount.vue";

const text = ref('')

useSeoMeta({
  title: 'Word Counter',
  ogTitle: 'Word Counter',
  description: 'Word Counter',
  ogDescription: 'Word Counter',
  ogImage: '',
})

const count = computed(() => {
  const textValue = text.value;
  const words: Number = textValue.trim().split(/\s+/).filter(word => word.length > 0).length;
  const chars = textValue.length;
  const charsNoSpaces = textValue.replace(/\s+/g, '').length;

  const sentences = textValue.split(/[.!?]+/).filter(sentence => sentence.trim().length > 0).length;
  const paragraphs = textValue.split(/\n\s*\n/).filter(paragraph => paragraph.length > 0).length;

  return {words, chars, charsNoSpaces, sentences, paragraphs};
});


</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Word Counter</h1>
        <p>Counts words, characters, sentences, and paragraphs.</p>
        <Textarea v-model="text" autofocus rows="10" class="w-full"
                  placeholder="Start typing, or copy and paste your text here..."/>
        <div class="mt-2">
          <WordCount title="Words" :value="count.words"/>
          <WordCount title="Characters" :value="count.chars"/>
          <WordCount title="Characters (no spaces)" :value="count.charsNoSpaces"/>
          <WordCount title="Sentences" :value="count.sentences"/>
          <WordCount title="Paragraphs" :value="count.paragraphs"/>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>