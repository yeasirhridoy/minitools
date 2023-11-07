<script setup>
useSeoMeta({
  title: 'BMI Calculator',
  ogTitle: 'BMI Calculator',
  description: 'BMI Calculator',
  ogDescription: 'BMI Calculator',
  ogImage: '',
})

const feet = ref()
const inches = ref()
const weight = ref()


const bmi = computed(() => {
  if (feet.value && inches.value && weight.value) {
    const heightInMeters = (feet.value * 0.3048) + (inches.value * 0.0254);
    const bmi = weight.value / (heightInMeters * heightInMeters);

    let status = ''
    if (bmi < 18.5) {
      status = 'Underweight'
    } else if (bmi >= 18.5 && bmi <= 24.9) {
      status = 'Normal'
    } else if (bmi >= 25 && bmi <= 29.9) {
      status = 'Overweight'
    } else if (bmi >= 30) {
      status = 'Obesity'
    }

    return 'Your BMI is ' + bmi.toFixed(2) + ' \nYour weight status is: ' + status;
  }
  return 'Fill in all the fields to calculate your BMI'
})
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>BMI Calculator</h1>
        <p>Calculate your BMI.</p>
        <div class="col-12">
          <div class="grid">
            <div class="col-12 md:col-6">
              <label for="from" class="font-bold mb-2">Your Height</label>
              <div class="p-inputgroup mt-2">
                <InputNumber id="from" v-model="feet" placeholder="Feet"/>
                <InputNumber id="to" v-model="inches" placeholder="Inches"/>
              </div>
            </div>
            <div class="col-12 md:col-6">
              <label for="to" class="font-bold mb-2">Your wight</label>
              <InputNumber id="to" v-model="weight" class="w-full mt-2" placeholder="Your weight in KG"/>
            </div>
            <div class="col-12">
              <div class="card flex flex-column">
                <h5>BMI Categories</h5>
                <div class="my-1">
                  Underweight = &lt;18.5
                </div>
                <div class="my-1">
                  Normal weight = 18.5–24.9
                </div>
                <div class="my-1">
                  Overweight = 25–29.9
                </div>
                <div class="my-1">
                  Obesity = BMI of 30 or greater
                </div>
              </div>
            </div>
            <div class="col-12">
              <SinglePreviewBox :text="bmi"/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>