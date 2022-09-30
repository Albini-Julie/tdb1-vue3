<script setup lang="ts">
import { checkbox } from "@formkit/inputs";
import { ref } from "@vue/reactivity";
import Card from "../components/card.vue";
import { supabase} from "../supabase";
import { useRouter } from "vue-router";
import {groupBy} from 'Lodash';
import {
    Disclosure,
    DisclosureButton,
    DisclosurePanel,
  } from '@headlessui/vue'
    
  const { data, error } = await supabase.from("quartiercommune").select("*");
    if (error) console.log("n'a pas pu charger la table quartiercommune :", error);

    
    

const router = useRouter();
//On fait une variable réactive qui référence les données
//ATTENTION : faire une Ref pas une Réactive car :
// c'est l'objet qui doit être réactif, pas ses props
const maison = ref({});



const props = defineProps(["id"]);
if (props.id) {
 // On charge les données de la maison
 let { data, error } = await supabase
 .from("maison")
 .select("*")
 .eq("id_maison", props.id);
 if (error) console.log("n'a pas pu charger le table Maison :", error);
 else maison.value = (data as any[])[0]};

 async function upsertMaison(dataForm, node) {
 const { data, error } = await supabase.from("maison").upsert(dataForm);
 if (error) node.setErrors([error.message])
 else {
 node.setErrors([]);
 router.push({ name: "edit-id", params: { id: data[0].id_maison } });
 }
};

const { data: dataQuartierCommune } = await supabase
  .from("quartiercommune")
  .select("*");
if (error) console.log("n'a pas pu charger la vue quartiercommune :", error);

const { data: dataAllAgent } = await supabase
  .from("allagent")
  .select("*");
if (error) console.log("n'a pas pu charger la vue Allagent :", error);

const optionsQuartier = dataQuartierCommune?.map((quartier) => ({
  value: quartier.code_Quartier,
  label: quartier.libelle_Quartier,
}));

const optionsAgent = dataAllAgent?.map((agent) => ({
  value: agent.id_agent,
  label: agent.last_name,
}));
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
            <FormKit type="form" @submit="upsertMaison" v-model="maison" submit-label="Envoyer" :submit-attrs="{ classes: { input: 'flex justify-center font-inter font-bold text-[20px] p-2 bg-indigo-500 text-white rounded mt-5' } }" :config="{classes: {
                    input: 'p-1 rounded border-indigo-500 shadow-sm border-2 hover:bg-indigo-100',
                    label: 'text-black font-inter font-semibold',
 },
}">
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="nom" label="Nom" placeholder="nom de la maison"/>
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="prix" label="Prix" type="number" placeholder="Prix de la maison"/>
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="bed" type="text" label="Chambres" placeholder="Nombre de chambre"/>
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="bath" type="text" label="Salles de bain" placeholder="Nombre de salle de bain"/>
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="size" type="text" label="Superficie" placeholder="Superfice de la maison"/>
                <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="image" type="text" label="Image" placeholder="Image de la maison"/>
                <FormKit wrapper-class="items-center flex flex-row-reverse my-3 justify-start gap-3 max-w-xs" name="préféré" label="Ajouter aux favoris" type="checkbox"/>



                <!--<FormKit name="code_Quartier" label="Quartier" type="select">
                    <optgroup v-for="(listeQuartier, libelle_Commune) in groupBy(data,'libelle_Commune')" :key="libelle_Commune" label={{libelle_Commune}}>     
                        <option value="{{ quartierObject.libelle_Quartier }}" v-for="quartierObject in listeQuartier" :key="quartierObject.code_Quartier" :disabled="true">{{ quartierObject.libelle_Quartier }}</option>
                    </optgroup>
                </FormKit>

                <FormKit name="id_agent" label="Agent" type="select">
                        <option v-for="agent in allagent" :key="id_agent" value="{{ agent.last_name }}">{{ agent.last_name }}</option>
                </FormKit>-->
                
                <option value="" :disabled="true">Choisir un quartier...</option>
                <FormKit
                    type="select"
                    name="code_Quartier"
                    label="Quartier"
                    :options="optionsQuartier"
                    wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs"
                />

                <option value="" :disabled="true">Choisir un agent...</option>
                <FormKit
                    type="select"
                    name="id_agent"
                    label="Agent"
                    :options="optionsAgent"
                    wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs"
                />
                
                
            </FormKit>

            
            

            

        </div>
    </div>
</template>