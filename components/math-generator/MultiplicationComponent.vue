<script setup>
import NumberMultiplication from './NumberMultiplication.vue';

const problems = ref([]);
const total = ref();
const min = ref();
const max = ref();
const level = ref();

const generateProblems = () => {

    const totalValue = total.value ? total.value : 10;
    const minValue = min.value > 0 ? min.value : 1;
    const maxValue = max.value > minValue ? max.value : minValue + 10000;
    const levelValue = level.value > 1 ? level.value : 2;

    problems.value = [];
    for (let i = 0; i < totalValue; i++) {
        const numbers = [];
        for (let j = 0; j < levelValue; j++) {
            numbers.push(Math.floor(Math.random() * (maxValue - minValue + 1) + minValue));
        }
        problems.value.push(numbers);
    }
};
</script>

<template>
    <div class="grid gap-2">
        <div class="col-12 md:col-2">
            <label for="min" class="font-bold mb-2">Minimum Value</label>
            <InputNumber id="min" v-model="min" class="w-full mt-2" placeholder="Minimum Value" />
        </div>
        <div class="col-12 md:col-2">
            <label for="max" class="font-bold mb-2">Maximum Value</label>
            <InputNumber id="max" v-model="max" class="w-full mt-2" placeholder="Maximum Value" />
        </div>
        <div class="col-12 md:col-2">
            <label for="level" class="font-bold mb-2">Level</label>
            <InputNumber id="level" v-model="level" class="w-full mt-2" placeholder="Level" />
        </div>
        <div class="col-12 md:col-2">
            <label for="total" class="font-bold mb-2">Total</label>
            <InputNumber id="total" v-model="total" class="w-full mt-2" placeholder="Total" />
        </div>
        <div class="col-12 md:col-2">
            <label class="font-bold mb-2">Generate Problems</label>
            <Button @click="generateProblems" class="w-full mt-2" icon="pi pi-arrow-right"
                    aria-label="Generate problems" />
        </div>

        <div class="col-12">
            <div class="grid gap-2">
                <NumberMultiplication v-for="(problem,i) in problems" :key="i" :numbers="problem" class="col-12 md:col-3"/>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">

</style>