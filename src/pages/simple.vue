<script setup lang="ts">
import Card from "../components/card.vue";
</script>


<template>
    <div class="p-2">
        <h2 class="text-2xl font-bold mb-5">Page simple</h2>
        <Card prix=2400 nom="Maison moderne" image="/public/pexels-binyamin-mellish-106399 1.jpg" préféré=true adresse="rue du Sapin" bed="3" bath="2" size="150m²"/>
    </div>
</template>