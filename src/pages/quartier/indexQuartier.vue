<script setup lang="ts">
    import { supabase } from "../../supabase";
    const { data, error } = await supabase.from("quartiercommune").select("*");
    if (error) console.log("n'a pas pu charger la table quartiercommune :", error);
    </script>
    
    <template>
      <section class="flex flex-col">
        <h3 class="text-2xl">Liste des quartiers</h3>
        <ul>
          <li v-for="quartierObject in (data as any[])">
            <DisclosureButton>{{ quartierObject.libelle_Commune }}
            </DisclosureButton> -
            {{ quartierObject.libelle_Quartier }}
          </li>
        </ul>

        <Disclosure
            v-for="(listeQuartier, libelle_Commune) in groupBy(
            data,
            'libelle_Commune'
            )" 
            :key="libelle_Commune"
        ></Disclosure>

  
  <DisclosurePanel>
    <ul><li
  v-for="quartierObject in listeQuartier"
  :key="quartierObject.code_Quartier"
></li>
</ul>
</DisclosurePanel>
        
      </section>
    </template>