<script setup lang="ts">
import {computed, onMounted, ref, watch} from "vue";
const COUNT = ref(1);
const array = ref<number[]>([]);
const checkedList = ref<boolean[]>([]);

const allSelected = computed({
    get() {
        return checkedList.value.length > 0 && checkedList.value.every(Boolean);
    },
    set(value: boolean) {
        checkedList.value = checkedList.value.map(() => value);
    }
});

function increment(val: number) {
    COUNT.value = val;
}

watch(() => COUNT.value, () => {
    array.value = new Array(COUNT.value).fill(0).map((_, i) => i);
    checkedList.value = array.value.map(() => false);
})

onMounted(() => {
    array.value = new Array(COUNT.value).fill(0).map((_, i) => i);
    checkedList.value = array.value.map(() => false);
});
</script>

<template>
    <div class="flex flex-col w-[80%] mx-auto mt-20">
        <h1 class="mb-5 text-xl font-bold">Total: {{COUNT}}</h1>
        <div class="flex mb-2">
            <input v-model="allSelected" type="checkbox" class="checkbox" />
            Select All
        </div>
        <div class="flex flex-wrap justify-items-start gap-2">
            <div v-for="(range, i) in array" :key="range" class="flex flex-1">
                <input v-model="checkedList[i]" type="checkbox" class="checkbox will-change-auto"/>
            </div>
        </div>
        <div class="flex mt-10 gap-5">
            <button class="btn btn-info btn-sm" @click="increment(1)">Set 1</button>
            <button class="btn btn-info btn-sm" @click="increment(10)">Set 10</button>
            <button class="btn btn-info btn-sm" @click="increment(50)">Set 50</button>
            <button class="btn btn-info btn-sm" @click="increment(100)">Set 100</button>
            <button class="btn btn-info btn-sm" @click="increment(1000)">Set 1000</button>
        </div>
    </div>

</template>

<style scoped>

</style>
