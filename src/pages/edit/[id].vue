<script setup lang="ts">
import type { DefineComponent } from "vue";
import Formulaire from "../../components/FormulaireMaison.vue";

const props = defineProps({
    id_maison: String
})
</script>


<template>
        <div class="p-2">
        <h2 class="text-2xl font-bold mb-5">New</h2>
        <Formulaire />
    </div>
</template>