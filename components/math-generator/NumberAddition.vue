<script setup>
const props = defineProps({
    numbers: {
        type: Array,
        required: true
    }
});

const answer = computed(() => {
    return props.numbers.reduce((a, b) => a + b, 0);
});

const showAnswer = ref(false);
</script>

<template>
    <div class="card">
        <span class="font-bold" v-for="(number, i) in numbers" :key="i">{{ number }}
            <span v-if="i < numbers.length - 1"> + </span>
        </span>
        <div v-if="!showAnswer">
            <Button @click="showAnswer = !showAnswer" :pt="{
                root: 'p-0',
            }" class="mt-4" size="small" text label="Show Answer" aria-label="Show answer" />
        </div>
        <div v-else class="font-bold mt-4"> = {{ answer }}</div>
    </div>
</template>

<style scoped lang="scss">

</style>