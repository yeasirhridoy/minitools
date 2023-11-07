<script setup>
const units = [
  {
    label: 'Celsius',
    value: 'c'
  },
  {
    label: 'Fahrenheit',
    value: 'f'
  },
  {
    label: 'Kelvin',
    value: 'k'
  }
]

const fromUnit = ref('c');
const toUnit = ref('f');
const inputValue = ref(null);

const outputValue = computed(() => {
  if (fromUnit.value && toUnit.value && inputValue.value) {
    const fromCelsiusValue = toCelsius(inputValue.value, fromUnit.value)
    return fromCelsius(fromCelsiusValue, toUnit.value)
  }
  return null
})

function toCelsius(value, unit) {
  switch (unit) {
    case 'c':
      return value
    case 'f':
      return (value - 32) * 5 / 9
    case 'k':
      return value - 273.15
  }
}

function fromCelsius(value, unit) {
  switch (unit) {
    case 'c':
      return value
    case 'f':
      return (value * 9 / 5) + 32
    case 'k':
      return value + 273.15
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