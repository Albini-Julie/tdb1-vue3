<script setup lang="ts">
import Formulaire from "../../components/FormulaireMaison.vue";

const props = defineProps({
    id: String
})
</script>


<template>
        <div class="p-2">
        <h2 class="text-2xl font-bold mb-5">Fiche récapitulative de la maison</h2>
        <Formulaire :id="id"/>
    </div>
</template>