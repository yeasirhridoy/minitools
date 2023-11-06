<script setup>

useSeoMeta({
  title: 'Password Generator',
  ogTitle: 'Password Generator',
  description: 'Password Generator',
  ogDescription: 'Password Generator',
  ogImage: '',
})

const password = ref('')
const length = ref(12)
const uppercase = ref(true)
const lowercase = ref(true)
const number = ref(true)
const symbol = ref(true)

const generatePassword = () => {
  const upperCaseLetters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
  const lowerCaseLetters = 'abcdefghijklmnopqrstuvwxyz'
  const numberLetters = '0123456789'
  const symbolLetters = '!@#$%^&*()_+='

  let allLetters = ''
  let generatedPassword = ''

  if (uppercase.value) {
    allLetters += upperCaseLetters
  }
  if (lowercase.value) {
    allLetters += lowerCaseLetters
  }
  if (number.value) {
    allLetters += numberLetters
  }
  if (symbol.value) {
    allLetters += symbolLetters
  }

  if (allLetters.length === 0) {
    password.value = 'You have to select at least one option.'
    return
  }
  for (let i = 0; i < length.value; i++) {
    generatedPassword += allLetters[Math.floor(Math.random() * allLetters.length)]
  }

  password.value = generatedPassword
}
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Password Generator</h1>
        <p>Generate random password for you.</p>
        <div class="flex align-items-center flex-wrap gap-2 p-fluid">
          <div class="flex-auto md:max-w-fit">
            <label for="paragraph" class="font-bold block mb-2">Password length</label>
            <InputNumber id="paragraph" class="flex-1" v-model="length" :min="1" :max="1000"/>
          </div>
          <div class="flex flex-wrap mt-2 md:mt-5 gap-4">
            <div class="flex">
              <InputSwitch id="uppercase" v-model="uppercase" name="uppercase"/>
              <label for="uppercase" class="ml-2"> Uppercase </label>
            </div>
            <div class="flex">
              <InputSwitch id="lowercase" v-model="lowercase" name="lowercase"/>
              <label for="lowercase" class="ml-2"> Lowercase </label>
            </div>
            <div class="flex">
              <InputSwitch id="number" v-model="number" name="number"/>
              <label for="number" class="ml-2"> Number </label>
            </div>
            <div class="flex">
              <InputSwitch id="symbol" v-model="symbol" name="symbol"/>
              <label for="symbol" class="ml-2"> Symbol </label>
            </div>
          </div>
          <Button class="flex-auto mt-2" @click="generatePassword()" label="Generate"/>
        </div>
        <SinglePreviewBox :text="password"/>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>