<script setup lang="ts">
    import { supabase } from "../../supabase";
    import {groupBy} from 'Lodash';
    import {
    Disclosure,
    DisclosureButton,
    DisclosurePanel,
  } from '@headlessui/vue'
    const { data, error } = await supabase.from("quartiercommune").select("*");
    if (error) console.log("n'a pas pu charger la table quartiercommune :", error);

    
    </script>
    
    <template>
      <section class="flex flex-col">
        <h3 class="text-2xl">Liste des quartiers</h3>
        <!---<ul>
          <li v-for="quartierObject in (data as any[])">
            {{ quartierObject.libelle_Commune }} -
            {{ quartierObject.libelle_Quartier }}
          </li>
        </ul>-->
  
        <Disclosure
            v-for="(listeQuartier, libelle_Commune) in groupBy(
            data,
            'libelle_Commune'
            )" 
            :key="libelle_Commune"
        >

        <DisclosureButton>{{libelle_Commune}}</DisclosureButton>
        <DisclosurePanel>
          <ul>
              <li
              v-for="quartierObject in listeQuartier"
              :key="quartierObject.code_Quartier"
              >
              {{quartierObject.libelle_Quartier}}
              </li>
          </ul>
       </DisclosurePanel>

</Disclosure>
  
  
        
      </section>
    </template>