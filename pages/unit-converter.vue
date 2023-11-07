<script setup>
import LengthConverter from "../components/unit-converter/LengthConverter.vue";
import AreaConverter from "../components/unit-converter/AreaConverter.vue";
import VolumeConverter from "../components/unit-converter/VolumeConverter.vue";
import WeightConverter from "../components/unit-converter/WeightConverter.vue";
import TemperatureConverter from "../components/unit-converter/TemperatureConverter.vue";
import TimeConverter from "../components/unit-converter/TimeConverter.vue";

useSeoMeta({
  title: 'Unit Converter',
  ogTitle: 'Unit Converter',
  description: 'Unit Converter',
  ogDescription: 'Unit Converter',
  ogImage: '',
})
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Unit Converter</h1>
        <p>Convert units from one to another.</p>

        <TabView>
          <TabPanel header="Length">
            <LengthConverter/>
          </TabPanel>
          <TabPanel header="Area">
            <AreaConverter/>
          </TabPanel>
          <TabPanel header="Volume">
            <VolumeConverter/>
          </TabPanel>
          <TabPanel header="Weight">
            <WeightConverter/>
          </TabPanel>
          <TabPanel header="Temperature">
            <TemperatureConverter/>
          </TabPanel>
          <TabPanel header="Time">
            <TimeConverter/>
          </TabPanel>
        </TabView>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>