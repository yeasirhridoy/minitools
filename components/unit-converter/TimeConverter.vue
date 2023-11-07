<script setup>
const units = [
  {
    label: 'Second',
    value: 's'
  },
  {
    label: 'Minute',
    value: 'min'
  },
  {
    label: 'Hour',
    value: 'h'
  },
  {
    label: 'Day',
    value: 'd'
  },
  {
    label: 'Week',
    value: 'week'
  },
  {
    label: 'Month',
    value: 'month'
  },
  {
    label: 'Year',
    value: 'year'
  },
  {
    label: 'Decade',
    value: 'decade'
  },
  {
    label: 'Century',
    value: 'century'
  }
]

const fromUnit = ref('s');
const toUnit = ref('min');
const inputValue = ref(null);

const outputValue = computed(() => {
  if (fromUnit.value && toUnit.value && inputValue.value) {
    const fromSecondValue = toSecond(inputValue.value, fromUnit.value)
    return fromSecond(fromSecondValue, toUnit.value)
  }
  return null
})

function toSecond(value, unit) {
  switch (unit) {
    case 's':
      return value
    case 'min':
      return value * 60
    case 'h':
      return value * 3600
    case 'd':
      return value * 86400
    case 'week':
      return value * 604800
    case 'month':
      return value * 2629800
    case 'year':
      return value * 31557600
    case 'decade':
      return value * 315576000
    case 'century':
      return value * 3155760000
  }
}

const fromSecond = (value, unit) => {
  switch (unit) {
    case 's':
      return value
    case 'min':
      return value / 60
    case 'h':
      return value / 3600
    case 'd':
      return value / 86400
    case 'week':
      return value / 604800
    case 'month':
      return value / 2629800
    case 'year':
      return value / 31557600
    case 'decade':
      return value / 315576000
    case 'century':
      return value / 3155760000
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