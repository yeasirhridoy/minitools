<script setup>
import AdditionComponent from '../components/math-generator/AdditionComponent.vue';
import SubtractionComponent from '../components/math-generator/SubtractionComponent.vue';
import MultiplicationComponent from '../components/math-generator/MultiplicationComponent.vue';
import DivisionComponent from '../components/math-generator/DivisionComponent.vue';

useSeoMeta({
  title: 'Math Generator',
  ogTitle: 'Math Generator',
  description: 'Generate basic math problems for practice.',
  ogDescription: 'Generate basic math problems for practice.',
  ogImage: '',
})
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Math Generator</h1>
        <p>Generate basic math problems for practice.</p>

        <TabView>
          <TabPanel header="Addition">
            <AdditionComponent/>
          </TabPanel>
          <TabPanel header="Subtraction">
            <SubtractionComponent/>
          </TabPanel>
          <TabPanel header="Multiplication">
            <MultiplicationComponent/>
          </TabPanel>
          <TabPanel header="Division">
            <DivisionComponent/>
          </TabPanel>
        </TabView>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>