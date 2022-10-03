<script setup lang="ts">
    import { checkbox } from "@formkit/inputs";
    import { ref } from "@vue/reactivity";
    
    import { supabase} from "../supabase";
    import { useRouter } from "vue-router";
    const router = useRouter();
    //On fait une variable réactive qui référence les données
    //ATTENTION : faire une Ref pas une Réactive car :
    // c'est l'objet qui doit être réactif, pas ses props
    const agent = ref({});
    
    
     async function upsertAgent(dataForm, node) {
     const { data, error } = await supabase.from("agent").upsert(dataForm);
     if (error) node.setErrors([error.message])
     else {
     alert("Agent enregistré")
     }
    };

    const props = defineProps(["id"]);
if (props.id) {
 // On charge les données du quartier
 let { data, error } = await supabase
 .from("agent")
 .select("*")
 .eq("id_agent", props.id);
 if (error) console.log("n'a pas pu charger le table Agent :", error);
 else agent.value = (data as any[])[0]};

 async function supprimerAgent() {
  const { data, error } = await supabase
    .from("agent")
    .delete()
    .match({ id_agent: agent.value.id_agent });
  if (error) {
    console.error(
      "Erreur à la suppression de ",
      agent.value,
      "erreur :",
      error
    );
  } else {
    router.push("/agent/indexAgent");
  }
}

const { data: listeUsers, error } = await supabase
  .from("allusers")
  .select("*");
if (error) console.log("n'a pas pu charger la table Users :", error);
// Les convertir par `map` en un tableau d'objets {value, label} pour FormKit
const optionsAgent = listeUsers?.map((users) => ({
  value: users.id,
  label: users.email,
}));

    </script>
    
    <template>
        <div>
            <div class="p-2">
                <!-- On passe la "ref" à FromKit-->
                <FormKit type="form" @submit="upsertAgent" submit-label="Envoyer" v-model="agent" :submit-attrs="{ classes: { input: 'flex justify-center font-inter font-bold text-[20px] p-2 bg-indigo-500 text-white rounded' } }" :config="{classes: {
                        input: 'p-1 rounded border-indigo-500 shadow-sm border-2 hover:bg-indigo-100',
                        label: 'text-black font-inter font-semibold',
     },
    }">
                    <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="first_name" label="Prénom" placeholder="Prénom de l'agent"/>
                    <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="last_name" label="Nom" placeholder="Nom de l'agent"/>

                    <FormKit
                    type="select"
                    name="id"
                    label="Utilisateur"
                    :options="optionsAgent"
                    
                />
            </FormKit>
                    
            
            </div>
            <button
        type="button"
        v-if="agent.id_agent"
        @click="($refs.dialogSupprimer as any).showModal()"
        class="focus-style justify-self-end rounded-md text-[20px] bg-red-500 p-2 font-inter font-bold text-white shadow-sm"
      >
        Supprimer l'agent
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
          @click="supprimerAgent()"
          class="focus-style rounded-md bg-red-500 p-2 shadow-sm"
        >
          Confirmer suppression
        </button>
      </dialog>
        </div>
    </template>