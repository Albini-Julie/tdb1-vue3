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
            v-for="(listeQuartier, libelle_Commune) in groupBy(
            data,
            'libelle_Commune'
            )" 
            :key="libelle_Commune"
        >

        
        <DisclosurePanel>
          <ul>
              <li>
              <RouterLink
                :to="{
                  name: 'commune-id',
                  params: { id: libelle_Commune.code_Commune },
                }"
              >{{ libelle_Commune }}
              </RouterLink>
              </li>
          </ul>
       </DisclosurePanel>

</Disclosure>


      
    </section>
  </template>