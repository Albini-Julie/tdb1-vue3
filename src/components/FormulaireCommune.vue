<script setup lang="ts">
    import { checkbox } from "@formkit/inputs";
    import { ref } from "@vue/reactivity";
    
    import { supabase} from "../supabase";
    import { useRouter } from "vue-router";
    const router = useRouter();
    //On fait une variable réactive qui référence les données
    //ATTENTION : faire une Ref pas une Réactive car :
    // c'est l'objet qui doit être réactif, pas ses props
    const commune = ref({});
    
    
     async function upsertCommune(dataForm, node) {
     const { data, error } = await supabase.from("commune").upsert(dataForm);
     if (error) node.setErrors([error.message])
     else {
     alert("Commune enregistrée")
     }
    };
    </script>
    
    <template>
        <div>
            <div class="p-2">
                <h2 class="text-2xl">Résultat (Prévisualisation)</h2>
                <!-- Optionnel on affiche les données-->
            </div>
            <div class="p-2">
                <!-- On passe la "ref" à FromKit-->
                <FormKit type="form" @submit="upsertCommune" submit-label="Envoyer" :submit-attrs="{ classes: { input: 'flex justify-center font-inter font-bold text-[20px] p-2 bg-indigo-500 text-white rounded' } }" :config="{classes: {
                        input: 'p-1 rounded border-indigo-500 shadow-sm border-2 hover:bg-indigo-100',
                        label: 'text-black font-inter font-semibold',
     },
    }">
                    <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="libelle_Commune" label="Nom" placeholder="nom de la commune"/>
                    
                </FormKit>
            </div>
        </div>
    </template>