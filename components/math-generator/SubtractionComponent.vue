<script setup>

import NumberSubtraction from './NumberSubtraction.vue';

const problems = ref([]);
const total = ref();
const min = ref();
const max = ref();

const generateProblems = () => {

    const totalValue = total.value ? total.value : 10;
    const minValue = min.value > 0 ? min.value : 1;
    const maxValue = max.value > minValue ? max.value : minValue + 100000;

    problems.value = [];
    for (let i = 0; i < totalValue; i++) {
        let largerNumber = Math.floor(Math.random() * (maxValue - minValue + 1) + minValue);
        let smallerNumber = Math.floor(Math.random() * (largerNumber - minValue + 1) + minValue);
        if (largerNumber < smallerNumber) {
            let temp = largerNumber;
            largerNumber = smallerNumber;
            smallerNumber = temp;
        }
        problems.value.push({ largerNumber, smallerNumber });
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
                <NumberSubtraction v-for="(problem,i) in problems" :key="i" :numbers="problem"
                                   class="col-12 md:col-3" />
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">

</style>