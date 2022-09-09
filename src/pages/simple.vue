<script setup lang="ts">
import Card from "../components/card.vue";

const maison1 = {
  nom: "Maison de campagne",
  prix: 2400,
  image: "/public/Mask Group.jpg",
  préféré: true,
  adresse: "Grand boulevard",
  bed: "2",
  bath: "1",
  size: "100m²",
};
</script>


<template>
    <div class="p-2">
        <h2 class="text-2xl font-bold mb-5">Page simple</h2>
        <Card :prix=2400 nom="Maison moderne" image="/public/pexels-binyamin-mellish-106399 1.jpg" :préféré=true adresse="rue du Sapin" bed="3" bath="2" size="150m²"/>
        <Card v-bind="maison1"/>
    </div>
</template>