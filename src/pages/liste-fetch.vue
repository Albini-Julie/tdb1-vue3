<script setup lang="ts">
import Card from "../components/card.vue";
const res = await fetch("/maisons.json");
const maisons = await res.json();
console.log(res);
</script>
    
<template>
     <div class="p-2">
        <h2 class="text-2xl font-bold mb-5">Page simple</h2>
        <Card v-for="maison in maisons" v-bind="maison" :key="maison.nom"/>
    </div>
</template>