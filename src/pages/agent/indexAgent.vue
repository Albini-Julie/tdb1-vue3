<script setup lang="ts">
    import { supabase } from "../../supabase";
    import {groupBy} from 'Lodash';
    import {
    Disclosure
  } from '@headlessui/vue'

    const { data, error } = await supabase.from("allagent").select("*");
    if (error) console.log("n'a pas pu charger la table allagent :", error);
  
    
    </script>
    
    <template>
      <section class="flex flex-col">
        <h3 class="text-2xl">Liste des agents</h3>
      
        <Disclosure
              v-for="(listeAgent, last_name) in groupBy(
              data,
              'last_name'
              )" 
              :key="last_name"
          >
  
          
          <DisclosurePanel>
            <ul>
                <li v-for="AgentObject in listeAgent"
                :key="AgentObject.id_agent">
                <RouterLink
                  :to="{
                    name: 'agent-id',
                    params: { id: AgentObject.id_agent },
                  }"
                >{{ AgentObject.last_name }}
                </RouterLink>
                </li>
            </ul>
         </DisclosurePanel>
  
  </Disclosure>
  
  
        
      </section>
    </template>