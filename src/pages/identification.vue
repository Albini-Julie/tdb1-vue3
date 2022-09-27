<script setup lang="ts">
    import { ref } from "@vue/reactivity";
    import { supabase, user } from "../supabase";
    async function signIn(data, node) {
      const { user, error } = await (nvlUtilisateur.value
        ? supabase.auth.signUp(data)
        : supabase.auth.signIn(data));
      if (error) {
        console.error(error);
        node.setErrors([error.message]);
      }
    }
    const nvlUtilisateur = ref(false);
    </script>
    <template>
      <div>
        <h2 class="text-2xl font-bold flex-wrap flex justify-center mb-8">Identification</h2>
        <button v-if="user" @pointerdown="supabase.auth.signOut()">
          Se déconnecter ({{ user.email }})
        </button>
        <FormKit
          v-else
          type="form"
          :submit-label="nvlUtilisateur ? 'S\'inscrire' : 'Se connecter'"
          @submit="signIn"
          :submit-attrs="{ classes: { input: 'flex justify-center font-inter font-bold text-[20px] p-2 bg-indigo-500 text-white rounded' } }" :config="{classes: {
                    input: 'p-1 rounded border-indigo-500 shadow-sm border-2 hover:bg-indigo-100',
                    label: 'text-black font-inter font-semibold',
 },
}"
          
          
        >
          <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="email" label="Votre eMail" type="email" />
          <FormKit wrapper-class="items-center flex m-5 justify-start gap-3 max-w-xs" name="password" label="Mot de passe" type="password" />
          <formKit
          wrapper-class="items-center flex flex-row-reverse my-3 justify-start gap-3 max-w-xs"
            label="Nouvel utilisateur ?"
            name="nvlUtilisateur"
            type="checkbox"
            v-model="nvlUtilisateur"
          />
        </FormKit>
      </div>
    </template>