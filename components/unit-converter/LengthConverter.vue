<script setup>
const units = [
  {
    label: 'Meter',
    value: 'm'
  },
  {
    label: 'Kilometer',
    value: 'km'
  },
  {
    label: 'Centimeter',
    value: 'cm'
  },
  {
    label: 'Millimeter',
    value: 'mm'
  },
  {
    label: 'Micrometer',
    value: 'μm'
  },
  {
    label: 'Nanometer',
    value: 'nm'
  },
  {
    label: 'Mile',
    value: 'mi'
  },
  {
    label: 'Yard',
    value: 'yd'
  },
  {
    label: 'Foot',
    value: 'ft'
  },
  {
    label: 'Inch',
    value: 'in'
  },
  {
    label: 'Light Year',
    value: 'ly'
  },
  {
    label: 'Nautical Mile',
    value: 'nmi'
  }
]

const fromUnit = ref('m');
const toUnit = ref('ft');
const inputValue = ref(null);

const outputValue = computed(() => {
  if (fromUnit.value && toUnit.value && inputValue.value) {
    const fromMeterValue = toMeter(inputValue.value, fromUnit.value)
    return fromMeter(fromMeterValue, toUnit.value)
  }
  return null
})

const toMeter = (value, unit) => {
  switch (unit) {
    case 'm':
      return value
    case 'km':
      return value * 1000
    case 'cm':
      return value / 100
    case 'mm':
      return value / 1000
    case 'μm':
      return value / 1000000
    case 'nm':
      return value / 1000000000
    case 'mi':
      return value * 1609.344
    case 'yd':
      return value * 0.9144
    case 'ft':
      return value * 0.3048
    case 'in':
      return value * 0.0254
    case 'ly':
      return value * 9460730472580800
    case 'nmi':
      return value * 1852
  }
}

const fromMeter = (value, unit) => {
  switch (unit) {
    case 'm':
      return value
    case 'km':
      return value / 1000
    case 'cm':
      return value * 100
    case 'mm':
      return value * 1000
    case 'μm':
      return value * 1000000
    case 'nm':
      return value * 1000000000
    case 'mi':
      return value / 1609.344
    case 'yd':
      return value / 0.9144
    case 'ft':
      return value / 0.3048
    case 'in':
      return value / 0.0254
    case 'ly':
      return value / 9460730472580800
    case 'nmi':
      return value / 1852
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