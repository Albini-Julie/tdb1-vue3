<script setup lang="ts">
import Card from "../components/card.vue";
const res = await fetch("/maisons.json");
const maisons = await res.json();
console.log(res);
defineProps<{ nbr: string }>();
</script>


<template>
    <div class="p-2">
        <h2 class="text-2xl font-bold mb-5">Offre</h2>
        <Card v-bind="maisons[Number(0)]" />
        <Card v-bind="maisons[Number(1)]" />
        <Card v-bind="maisons[Number(2)]" />
    </div>
</template>