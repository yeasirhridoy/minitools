<script setup>
const props = defineProps({
    numbers: {
        type: Object,
        required: true
    }
});

const answer = computed(() => {
    return props.numbers?.largerNumber - props.numbers?.smallerNumber;
});

const showAnswer = ref(false);

watch(() => props.numbers, () => {
    showAnswer.value = false;
});
</script>

<template>
    <div class="card mb-1">
        <span class="font-bold">
            {{ numbers?.largerNumber }} - {{ numbers?.smallerNumber }}
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