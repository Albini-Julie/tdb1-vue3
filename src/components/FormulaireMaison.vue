<script setup lang="ts">
import { checkbox } from "@formkit/inputs";
import { ref } from "@vue/reactivity";
import Card from "../components/card.vue";
//On fait une variable réactive qui référence les données
//ATTENTION : faire une Ref pas une Réactive car :
// c'est l'objet qui doit être réactif, pas ses props
const maison = ref({});
</script>

<template>
    <div>
        <div class="p-2">
            <h2 class="text-2xl">Résultat (Prévisualisation)</h2>
            <!-- Optionnel on affiche les données-->
            <Card v-bind="maison"/>
        </div>
        <div class="p-2">
            <!-- On passe la "ref" à FromKit-->
            <FormKit type="form" v-model="maison" submit-label="Envoyer" :submit-attrs="{ classes: { input: 'flex justify-center font-inter font-bold text-[20px] p-2 bg-indigo-500 text-white rounded' } }" :config="{classes: {
                    input: 'p-1 rounded border-indigo-500 shadow-sm border-2 hover:bg-indigo-100',
                    label: 'text-black font-inter font-semibold',
 },
}">
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="nom" label="Nom" placeholder="nom de la maison"/>
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="prix" label="Prix" type="number" placeholder="Prix de la maison"/>
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="bed" type="text" label="Chambres" placeholder="Nombre de chambre"/>
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="bath" type="text" label="Salles de bain" placeholder="Nombre de salle de bain"/>
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="size" type="text" label="Superficie" placeholder="Superfice de la maison"/>
                <FormKit wrapper-class="items-center flex flex-row-reverse my-3 justify-start gap-3 max-w-xs" name="préféré" label="Ajouter aux favoris" type="checkbox"/>
                
            </FormKit>
        </div>
    </div>
</template>