<script setup lang="ts">
  import { supabase } from "../../supabase";
  import {groupBy} from 'Lodash';
  import {
  Disclosure
} from '@headlessui/vue'
  const { data, error } = await supabase.from("allcommunes").select("*");
  if (error) console.log("n'a pas pu charger la table allcommunes :", error);

  
  </script>
  
  <template>
    <section class="flex flex-col">
      <h3 class="text-2xl">Liste des Communes</h3>
    
      <Disclosure
            v-for="(listeCommune, libelle_Commune) in groupBy(
            data,
            'libelle_Commune'
            )" 
            :key="libelle_Commune"
        >

        
        <DisclosurePanel>
          <ul>
              <li v-for="CommuneObject in listeCommune"
              :key="CommuneObject.code_Commune">
              <RouterLink
                :to="{
                  name: 'commune-id',
                  params: { id: CommuneObject.code_Commune },
                }"
              >{{ CommuneObject.libelle_Commune }}
              </RouterLink>
              </li>
          </ul>
       </DisclosurePanel>

</Disclosure>


      
    </section>
  </template>