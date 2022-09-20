<script setup lang="ts">
import Card from "../components/card.vue";
import { supabase } from "../supabase";
console.log("supabase :", supabase); // pour vérifier et "garder" supabase dans le code
const maisons = []; // à remplacer par l'appel à Supabase

let { data: maison, error } = await supabase
  .from('maison')
  .select('*')
</script>
    
<template>
     <div class="p-2">
        <h2 class="text-2xl font-bold mb-5">Page simple</h2>
        <Card v-for="maison in maisons" v-bind="maison" :key="maison.nom"/>
    </div>
</template>