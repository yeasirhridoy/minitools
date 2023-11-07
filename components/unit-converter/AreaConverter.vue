<script setup>
const units = [
  {
    label: 'Square Meter',
    value: 'm2'
  },
  {
    label: 'Square Kilometer',
    value: 'km2'
  },
  {
    label: 'Square Centimeter',
    value: 'cm2'
  },
  {
    label: 'Square Millimeter',
    value: 'mm2'
  },
  {
    label: 'Square Micrometer',
    value: 'μm2'
  },
  {
    label: 'Square Mile',
    value: 'mi2'
  },
  {
    label: 'Square Yard',
    value: 'yd2'
  },
  {
    label: 'Square Foot',
    value: 'ft2'
  },
  {
    label: 'Square Inch',
    value: 'in2'
  },
  {
    label: 'Hectare',
    value: 'ha'
  },
  {
    label: 'Acre',
    value: 'ac'
  }
]

const fromUnit = ref('m2');
const toUnit = ref('ft2');
const inputValue = ref(null);

const outputValue = computed(() => {
  if (fromUnit.value && toUnit.value && inputValue.value) {
    const fromMeterValue = toSquareMeter(inputValue.value, fromUnit.value)
    return fromSquareMeter(fromMeterValue, toUnit.value)
  }
  return null
})

const toSquareMeter = (value, unit) => {
  switch (unit) {
    case 'm2':
      return value
    case 'km2':
      return value * 1000000
    case 'cm2':
      return value / 10000
    case 'mm2':
      return value / 1000000
    case 'μm2':
      return value / 1000000000000
    case 'mi2':
      return value * 2589988.110336
    case 'yd2':
      return value / 1.1959900463011
    case 'ft2':
      return value / 10.76391041671
    case 'in2':
      return value / 1550.0031000062
    case 'ha':
      return value * 10000
    case 'ac':
      return value * 4046.8564224
    default:
      return null
  }
}

const fromSquareMeter = (value, unit) => {
  switch (unit) {
    case 'm2':
      return value
    case 'km2':
      return value / 1000000
    case 'cm2':
      return value * 10000
    case 'mm2':
      return value * 1000000
    case 'μm2':
      return value * 1000000000000
    case 'mi2':
      return value / 2589988.110336
    case 'yd2':
      return value * 1.1959900463011
    case 'ft2':
      return value * 10.76391041671
    case 'in2':
      return value * 1550.0031000062
    case 'ha':
      return value / 10000
    case 'ac':
      return value / 4046.8564224
    default:
      return null
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