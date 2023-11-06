<script setup>

useSeoMeta({
  title: 'Age Calculator',
  ogTitle: 'Age Calculator',
  description: 'Age Calculator',
  ogDescription: 'Age Calculator',
  ogImage: '',
})

const startDate = ref();
const endDate = ref(new Date());

const age = computed(() => {
  const start = new Date(startDate.value);
  const end = new Date(endDate.value);
  let year = end.getFullYear() - start.getFullYear();
  let month = end.getMonth() - start.getMonth();
  let day = end.getDate() - start.getDate();
  if (day < 0) {
    month--;
    switch (start.getMonth()) {
      case 0:
        day += 31;
        break;
      case 1:
        if (start.getFullYear() % 4 === 0) {
          day += 29;
        } else {
          day += 28;
        }
        break;
      case 2:
        day += 31;
        break;
      case 3:
        day += 30;
        break;
      case 4:
        day += 31;
        break;
      case 5:
        day += 30;
        break;
      case 6:
        day += 31;
        break;
      case 7:
        day += 31;
        break;
      case 8:
        day += 30;
        break;
      case 9:
        day += 31;
        break;
      case 10:
        day += 30;
        break;
      case 11:
        day += 31;
        break;
    }
  }
  if (month < 0) {
    year--;
    month += 12;
  }
  const ageInMonths = year * 12 + month;
  const ageInDays = Math.floor((end.getTime() - start.getTime()) / (1000 * 3600 * 24));

  return {
    year,
    ageInMonths,
    ageInDays,
    month,
    day
  };
});
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Age Calculator</h1>
        <p>Calculate your age in years, months, and days.</p>
        <div class="grid gap-2">
          <div class="p-inputgroup flex-1">
          <span class="p-inputgroup-addon w-8rem">
              Date of Birth
            </span>
            <Calendar v-model="startDate" date-format="d M yy" show-icon placeholder="Select a date"/>
          </div>
          <div class="p-inputgroup flex-1">
          <span class="p-inputgroup-addon w-8rem">
              Compare with
            </span>
            <Calendar v-model="endDate" date-format="d M yy" show-icon placeholder="Select a date"/>
          </div>
        </div>
        <div class="grid mt-4" v-if="startDate && endDate">
          <div class="col-12">
            Age: {{ age.year }} years, {{ age.month }} months, {{ age.day }} days
          </div>
          <div class="col-12">
            Age in months: {{ age.ageInMonths }}
          </div>
          <div class="col-12">
            Age in days: {{ age.ageInDays }}
          </div>
        </div>
        <div v-else class="mt-4">
          Select a date to compare
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>