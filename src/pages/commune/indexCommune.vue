<script setup lang="ts">
    import { supabase } from "../../supabase";
    import {groupBy} from 'Lodash';
    import {
    Disclosure,
    DisclosureButton,
    DisclosurePanel,
  } from '@headlessui/vue'
    const { data, error } = await supabase.from("commune").select("*");
    if (error) console.log("n'a pas pu charger la table commune :", error);

    
    </script>
    
    <template>
      <section class="flex flex-col">
        <h3 class="text-2xl">Liste des Communes</h3>
  
        <div
            v-for="(libelle_Commune) in
            commune.libelle_Commune"
            :key="libelle_Commune"
        >
        

      </div>
  
  
        
      </section>
    </template>