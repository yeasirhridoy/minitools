<script setup>
const units = [
  {
    label: 'Kilogram',
    value: 'kg'
  },
  {
    label: 'Gram',
    value: 'g'
  },
  {
    label: 'Milligram',
    value: 'mg'
  },
  {
    label: 'Microgram',
    value: 'μg'
  },
  {
    label: 'Imperial Ton',
    value: 'imperial_ton'
  },
  {
    label: 'US Ton',
    value: 'us_ton'
  },
  {
    label: 'Stone',
    value: 'stone'
  },
  {
    label: 'Pound',
    value: 'lb'
  },
  {
    label: 'Ounce',
    value: 'oz'
  }
]

const fromUnit = ref('kg');
const toUnit = ref('lb');
const inputValue = ref(null);

const outputValue = computed(() => {
  if (fromUnit.value && toUnit.value && inputValue.value) {
    const fromKilogramValue = toKilogram(inputValue.value, fromUnit.value)
    return fromKilogram(fromKilogramValue, toUnit.value)
  }
  return null
})

function toKilogram(value, unit) {
  switch (unit) {
    case 'kg':
      return value
    case 'g':
      return value / 1000
    case 'mg':
      return value / 1000000
    case 'μg':
      return value / 1000000000
    case 'imperial_ton':
      return value * 1016.05
    case 'us_ton':
      return value * 907.185
    case 'stone':
      return value * 6.35029
    case 'lb':
      return value * 0.453592
    case 'oz':
      return value * 0.0283495
  }
}

function fromKilogram(value, unit) {
  switch (unit) {
    case 'kg':
      return value
    case 'g':
      return value * 1000
    case 'mg':
      return value * 1000000
    case 'μg':
      return value * 1000000000
    case 'imperial_ton':
      return value / 1016.05
    case 'us_ton':
      return value / 907.185
    case 'stone':
      return value / 6.35029
    case 'lb':
      return value / 0.453592
    case 'oz':
      return value / 0.0283495
  }
}

const switchUnit = () => {
  const temp = fromUnit.value
  fromUnit.value = toUnit.value
  toUnit.value = temp
}
</script>

<template>
  <div class="grid gap-2">
    <div class="col-12">
      <div class="grid">
        <div class="col-12 md:col-8">
          <div class="grid">
            <div class="col-12 md:col-5">
              <label for="from" class="font-bold mb-2">From</label>
              <Dropdown id="from" :options="units" v-model="fromUnit" option-label="label" option-value="value"
                        class="w-full mt-2" placeholder="Choose a unit"/>
            </div>
            <div class="col-12 md:col-2">
              <label class="font-bold mb-2">Switch</label>
              <Button @click="switchUnit" class="w-full mt-2" icon="pi pi-arrow-right-arrow-left" aria-label="Filter" />
            </div>
            <div class="col-12 md:col-5">
              <label for="to" class="font-bold mb-2">To</label>
              <Dropdown id="to" :options="units" v-model="toUnit" option-label="label" option-value="value"
                        class="w-full mt-2" placeholder="Choose a unit"/>
            </div>
          </div>
        </div>
        <div class="col-12 md:col-4">
          <label for="input" class="font-bold mb-2">Value</label>
          <InputNumber id="input" v-model="inputValue" class="w-full mt-2" placeholder="Enter a value"/>
        </div>
      </div>
    </div>
    <div class="col-12">
      <SinglePreviewBox :text="outputValue"/>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>