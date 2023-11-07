<script setup>
const units = [
  {
    label: 'Cubic Meter',
    value: 'm3'
  },
  {
    label: 'Cubic Kilometer',
    value: 'km3'
  },
  {
    label: 'Cubic Centimeter',
    value: 'cm3'
  },
  {
    label: 'Cubic Millimeter',
    value: 'mm3'
  },
  {
    label: 'Liter',
    value: 'l'
  },
  {
    label: 'Milliliter',
    value: 'ml'
  },
  {
    label: 'Gallon',
    value: 'gal'
  },
  {
    label: 'Quart',
    value: 'qt'
  },
  {
    label: 'Pint',
    value: 'pt'
  },
  {
    label: 'Cup',
    value: 'cup'
  },
  {
    label: 'Fluid Ounce',
    value: 'fl oz'
  },
  {
    label: 'Tablespoon',
    value: 'tbsp'
  },
  {
    label: 'Teaspoon',
    value: 'tsp'
  },
  {
    label: 'Cubic Mile',
    value: 'mi3'
  },
  {
    label: 'Cubic Yard',
    value: 'yd3'
  },
  {
    label: 'Cubic Foot',
    value: 'ft3'
  },
  {
    label: 'Cubic Inch',
    value: 'in3'
  }
]

const fromUnit = ref('m3');
const toUnit = ref('l');
const inputValue = ref(null);

const outputValue = computed(() => {
  if (fromUnit.value && toUnit.value && inputValue.value) {
    const fromMeterValue = toCubicMeter(inputValue.value, fromUnit.value)
    return fromCubicMeter(fromMeterValue, toUnit.value)
  }
  return null
})

const toCubicMeter = (value, unit) => {
  switch (unit) {
    case 'm3':
      return value
    case 'km3':
      return value * 1e9
    case 'cm3':
      return value / 1e6
    case 'mm3':
      return value / 1e9
    case 'l':
      return value / 1000
    case 'ml':
      return value / 1e6
    case 'gal':
      return value / 264.172
    case 'qt':
      return value / 1056.69
    case 'pt':
      return value / 2113.38
    case 'cup':
      return value / 4226.75
    case 'fl oz':
      return value / 33814
    case 'tbsp':
      return value / 67628
    case 'tsp':
      return value / 202884
    case 'mi3':
      return value * 4.168e9
    case 'yd3':
      return value / 1.308
    case 'ft3':
      return value / 35.315
    case 'in3':
      return value / 61024
  }
}

const fromCubicMeter = (value, unit) => {
  switch (unit) {
    case 'm3':
      return value
    case 'km3':
      return value / 1e9
    case 'cm3':
      return value * 1e6
    case 'mm3':
      return value * 1e9
    case 'l':
      return value * 1000
    case 'ml':
      return value * 1e6
    case 'gal':
      return value * 264.172
    case 'qt':
      return value * 1056.69
    case 'pt':
      return value * 2113.38
    case 'cup':
      return value * 4226.75
    case 'fl oz':
      return value * 33814
    case 'tbsp':
      return value * 67628
    case 'tsp':
      return value * 202884
    case 'mi3':
      return value / 4.168e9
    case 'yd3':
      return value * 1.308
    case 'ft3':
      return value * 35.315
    case 'in3':
      return value * 61024
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
              <Button @click="switchUnit" class="w-full mt-2" icon="pi pi-arrow-right-arrow-left" aria-label="Filter"/>
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