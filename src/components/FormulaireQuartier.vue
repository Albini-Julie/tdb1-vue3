<script setup lang="ts">
    import { checkbox } from "@formkit/inputs";
    import { ref } from "@vue/reactivity";
    
    import { supabase} from "../supabase";
    import { useRouter } from "vue-router";
    const router = useRouter();
    //On fait une variable réactive qui référence les données
    //ATTENTION : faire une Ref pas une Réactive car :
    // c'est l'objet qui doit être réactif, pas ses props
    const quartier = ref({});
    
    
     async function upsertQuartier(dataForm, node) {
     const { data, error } = await supabase.from("quartier").upsert(dataForm);
     if (error) node.setErrors([error.message])
     else {
     alert("Quartier enregistré")
     }
    };

    const props = defineProps(["id"]);
if (props.id) {
 // On charge les données du quartier
 let { data, error } = await supabase
 .from("quartier")
 .select("*")
 .eq("code_Quartier", props.id);
 if (error) console.log("n'a pas pu charger le table Quartier :", error);
 else quartier.value = (data as any[])[0]};

 const { data: listeCommune, error } = await supabase
  .from("commune")
  .select("*");
if (error) console.log("n'a pas pu charger la table Commune :", error);
// Les convertir par `map` en un tableau d'objets {value, label} pour FormKit
const optionsCommune = listeCommune?.map((commune) => ({
  value: commune.code_Commune,
  label: commune.libelle_Commune,
}));

    </script>
    
    <template>
        <div>
            <div class="p-2">
                <!-- On passe la "ref" à FromKit-->
                <FormKit type="form" @submit="upsertQuartier" submit-label="Envoyer" v-model="quartier" :submit-attrs="{ classes: { input: 'flex justify-center font-inter font-bold text-[20px] p-2 bg-indigo-500 text-white rounded' } }" :config="{classes: {
                        input: 'p-1 rounded border-indigo-500 shadow-sm border-2 hover:bg-indigo-100',
                        label: 'text-black font-inter font-semibold',
     },
    }">
                    <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="libelle_Quartier" label="Nom" placeholder="nom du quartier"/>
                    
                </FormKit>

                <!-- Affiche les communes avec comme valeur l'id de la relation -->
                <FormKit
                    type="select"
                    name="code_Commune"
                    label="Commune"
                    :options="optionsCommune"
                />
            </div>
        </div>
    </template>