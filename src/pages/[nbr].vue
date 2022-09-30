<script setup lang="ts">
import Card from "../components/card.vue";
const res = await fetch("/maisons.json");
const maisons = await res.json();
console.log(res);
defineProps<{ nbr: string }>();
</script>


<template>
    <div class="p-2">
        <h2 class="text-2xl font-bold flex-wrap flex justify-center mb-8"
>Offre</h2>
        <div class="gap-5 grid grid-flow-row-dense grid-auto-flow grid-cols-[repeat(auto-fit,minmax(200px,1fr))]">
        <Card v-bind="maisons[Number(0)]" />
        <Card v-bind="maisons[Number(1)]" />
        <Card v-bind="maisons[Number(2)]" />
        </div>
    </div>
</template>