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

async function supprimerQuartier() {
  const { data, error } = await supabase
    .from("quartier")
    .delete()
    .match({ code_Quartier: quartier.value.code_Quartier });
  if (error) {
    console.error(
      "Erreur à la suppression de ",
      quartier.value,
      "erreur :",
      error
    );
  } else {
    router.push("/quartier/indexQuartier");
  }
}

    </script>
    
    <template>
        <div>
            <div class="p-2">
                <!-- On passe la "ref" à FromKit-->
                <FormKit type="form" @submit="upsertQuartier" submit-label="Envoyer" v-model="quartier" :submit-attrs="{ classes: { input: 'flex justify-center font-inter font-bold text-[20px] p-2 bg-indigo-500 text-white rounded my-5' } }" :config="{classes: {
                        input: 'p-1 rounded border-indigo-500 shadow-sm border-2 hover:bg-indigo-100',
                        label: 'text-black font-inter font-semibold',
     },
    }">
                    <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="libelle_Quartier" label="Nom" placeholder="nom du quartier"/>
                    

                <!-- Affiche les communes avec comme valeur l'id de la relation -->
                <FormKit
                    type="select"
                    name="code_Commune"
                    label="Commune"
                    :options="optionsCommune"
                    
                />
            </FormKit>

            </div>
            <button
        type="button"
        v-if="quartier.code_Quartier"
        @click="($refs.dialogSupprimer as any).showModal()"
        class="focus-style justify-self-end rounded-md text-[20px] bg-red-500 p-2 font-inter font-bold text-white shadow-sm"
      >
        Supprimer le quartier
      </button>
      <dialog
        ref="dialogSupprimer"
        @click="($event.currentTarget as any).close()"
      >
        <button
          type="button"
          class="focus-style justify-self-end rounded-md bg-blue-300 p-2 shadow-sm"
        >
          Annuler</button
        ><button
          type="button"
          @click="supprimerQuartier()"
          class="focus-style rounded-md bg-red-500 p-2 shadow-sm"
        >
          Confirmer suppression
        </button>
      </dialog>
        </div>
    </template>