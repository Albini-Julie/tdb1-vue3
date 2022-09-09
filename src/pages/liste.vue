<script setup lang="ts">
import Card from "../components/card.vue";

const maisons = [
  {
    nom: "Maison de campagne",
    prix: 2400,
    image: "/public/Mask Group.jpg",
    préféré: true,
    adresse: "Grand boulevard",
    bed: "2",
    bath: "1",
    size: "100m²",
  },
  {
    nom: "Maison moderne",
    prix: 2400,
    image: "/public/pexels-binyamin-mellish-106399 1.jpg",
    préféré: true,
    adresse: "rue du Sapin",
    bed: "3",
    bath: "2",
    size: "150m²",
  },
  {
    nom: "Maison périphérie",
    prix: 1750,
    image: "/public/Mask Group.jpg",
    préféré: false,
    adresse: "Périphérie de ville",
    bed: "4",
    bath: "3",
    size: "200m²",
  },
  {
    nom: "Maison parfaite",
    prix: 5000,
    image: "/public/pexels-binyamin-mellish-106399 1.jpg",
    préféré: false,
    adresse: "rue Simone Veil",
    bed: "4",
    bath: "2",
    size: "180m²",
  },
];
</script>

<template>
     <div class="p-2">
        <h2 class="text-2xl font-bold mb-5">Page simple</h2>
        <Card v-for="maison in maisons" v-bind="maison" :key="maison.nom"/>
    </div>
</template>