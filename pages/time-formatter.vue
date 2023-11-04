<script setup>

import FormattedTime from "../components/time-formatter/FormattedTime.vue";

const timestamp = ref(new Date());
const formatDate = (format) => {
  const date = timestamp.value;
  const parts = {
    'YYYY': date.getFullYear(),
    'M': date.getMonth() + 1,
    'MM': String(date.getMonth() + 1).padStart(2, '0'),
    'MMM': getShortMonthName(date.getMonth()),
    'MMMM': getMonthName(date.getMonth()),
    'D': date.getDate(),
    'DD': String(date.getDate()).padStart(2, '0'),
    'DDD': getShortDayName(date.getDay()),
    'DDDD': getDayName(date.getDay()),
    'H': date.getHours(),
    'HH': String(date.getHours()).padStart(2, '0'),
    'h': date.getHours() % 12,
    'hh': String(date.getHours() % 12).padStart(2, '0'),
    'm': date.getMinutes(),
    'mm': String(date.getMinutes()).padStart(2, '0'),
    's': date.getSeconds(),
    'ss': String(date.getSeconds()).padStart(2, '0'),
    'a': date.getHours() >= 12 ? 'pm' : 'am',
    'A': date.getHours() >= 12 ? 'PM' : 'AM',
  };

  return format.replace(/(YYYY|MMMM|MMM|MM|M|DDDD|DDD|DD|D|HH|H|hh|h|mm|m|ss|s|a|A)/g, match => {
    return parts[match];
  });
};

const getDateInMilliseconds = () => {
  return timestamp.value.getTime();
};

const getMonthName = (monthIndex) => {
  const months = [
    'January', 'February', 'March', 'April',
    'May', 'June', 'July', 'August',
    'September', 'October', 'November', 'December'
  ];
  return months[monthIndex];
};

const getShortMonthName = (monthIndex) => {
  const shortMonths = [
    'Jan', 'Feb', 'Mar', 'Apr',
    'May', 'Jun', 'Jul', 'Aug',
    'Sep', 'Oct', 'Nov', 'Dec'
  ];
  return shortMonths[monthIndex];
};

const getDayName = (dayIndex) => {
  const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
  return days[dayIndex];
};

const getShortDayName = (dayIndex) => {
  const shortDays = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
  return shortDays[dayIndex];
};

const formattedTimes = computed(() => {
  return [
    formatDate('M/DD/YYYY HH:mm:ss A'),
    formatDate('MMMM DDDD YYYY, h:mm:ss A'),
    formatDate('MMM DD YYYY, h:mm:ss A'),
    getDateInMilliseconds()
  ];
})
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Time Formatter</h1>
        <div class="p-inputgroup flex-1 w-fit mb-4">
          <Calendar id="calendar-12h" v-model="timestamp" showTime hourFormat="12" placeholder="Select a time"/>
        </div>
        <h4 class="mt-2">Output</h4>
        <div class="border-1 border-round border-gray-300 p-2" style="min-height: 64px">
          <FormattedTime v-for="(time,i) in formattedTimes" :key="i" :time="time"/>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>