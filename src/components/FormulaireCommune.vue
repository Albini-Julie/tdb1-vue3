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

    const props = defineProps(["id"]);
if (props.id) {
 // On charge les données du quartier
 let { data, error } = await supabase
 .from("commune")
 .select("*")
 .eq("code_Commune", props.id);
 if (error) console.log("n'a pas pu charger le table Commune :", error);
 else commune.value = (data as any[])[0]};

 async function supprimerCommune() {
  const { data, error } = await supabase
    .from("commune")
    .delete()
    .match({ code_Commune: commune.value.code_Commune });
  if (error) {
    console.error(
      "Erreur à la suppression de ",
      commune.value,
      "erreur :",
      error
    );
  } else {
    router.push("/commune/indexCommune");
  }
}
    </script>
    
    <template>
        <div>
            <div class="p-2">
                <!-- On passe la "ref" à FromKit-->
                <FormKit type="form" @submit="upsertCommune" submit-label="Envoyer" v-model="commune" :submit-attrs="{ classes: { input: 'flex justify-center font-inter font-bold text-[20px] p-2 bg-indigo-500 text-white rounded' } }" :config="{classes: {
                        input: 'p-1 rounded border-indigo-500 shadow-sm border-2 hover:bg-indigo-100',
                        label: 'text-black font-inter font-semibold',
     },
    }">
                    <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="libelle_Commune" label="Nom" placeholder="nom de la commune"/>
                </FormKit>
            </div>
            <button
        type="button"
        v-if="commune.code_Commune"
        @click="($refs.dialogSupprimer as any).showModal()"
        class="focus-style justify-self-end rounded-md text-[20px] bg-red-500 p-2 font-inter font-bold text-white shadow-sm"
      >
        Supprimer la commune
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
          @click="supprimerCommune()"
          class="focus-style rounded-md bg-red-500 p-2 shadow-sm"
        >
          Confirmer suppression
        </button>
      </dialog>
        </div>
    </template>