<template>
<div class="mb-5 flex flex-wrap justify-between">
<button class="relative z-50 m-5" aria-controls="menu" :aria-expanded="menuOuvert" @click="menuOuvert = !menuOuvert " 
:class="[menuOuvert ? 'hidden' : '',]">
  <Menu1 class="mx-5" />
      <span class="sr-only">Menu</span>
    </button>
    <button class="relative z-50 m-5" aria-controls="menu" :aria-expanded="menuOuvert" @click="menuOuvert = !menuOuvert " 
:class="[menuOuvert ? '' : 'hidden',]">
  <Croix class="mx-5" />
      <span class="sr-only">Menu</span>
    </button>
</div>

    <div class="fixed inset-0 translate-x-full motion-safe:transition-transform motion-safe:duration-1000"
    :class="['bg-gray-900 text-white', menuOuvert ? 'translate-x-0' : '',]">
    <div class="flex justify-center items-center">
      <ul class="sm:flex "  @click="menuOuvert = !menuOuvert ">
        <div class="flex flex-col mt-10">
          <router-link to="/">
          <h2 class="font-bold text-2xl">Agence Immobilirère</h2>
        </router-link>
          <li class="mt-5" :class="[menuOuvert ? '' : 'hidden',]">
            <router-link class="" to="/simple">
                Simple
            </router-link>
          </li>
          <li class="mt-5">
            <router-link class="" to="/liste">
                Liste
            </router-link>
          </li>
          <li class="mt-5">
        
        <router-link class="" to="/liste-fetch">
            Liste-fetch
            
          </router-link>
        
        </li>

        <li class="mt-5">
        
        <router-link class="" to="/[nbr]">
            Offre
            
          </router-link>
        
        </li>
        <li class="mt-5">
        
        <router-link class="" to="/edit/new">
            Nouvelle maison
            
          </router-link>
        
        </li>

        <li class="mt-5">
        
        <router-link class="" to="/edit/new_commune">
            Nouvelle commune
            
          </router-link>
        
        </li>

        <li class="mt-5">
        
        <router-link class="" to="/edit/new_quartier">
            Nouveau quartier
            
          </router-link>
        
        </li>

        <li class="mt-5">
        
        <router-link class="" to="/edit/new_agent">
            Nouvel agent
            
          </router-link>
        
        </li>

        <li class="mt-5">
        
        <router-link class="" to="/list-supabase">
            liste-supabase
            
          </router-link>
        
        </li>

        <li class="mt-5">
        
        <router-link class="" to="/identification">
            identification
            
          </router-link>
        
        </li>

        <li class="mt-5">
        
        <router-link class="" to="/quartier/indexQuartier">
            QuartierCommune
            
          </router-link>
        
        </li>

        </div>
      </ul>
    </div>
  </div>





  <!-- Affiche les pages -->
  <Suspense>
  <router-view class="m-2 border-2 p-2" />
</Suspense>
</template>

<script setup>
  import Menu1 from "./components/icones/menu.vue"
  import Croix from "./components/icones/croix.vue"
  import { ref } from "vue";
  let menuOuvert = ref()
  menuOuvert.value = false
</script>
