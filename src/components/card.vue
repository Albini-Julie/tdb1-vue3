<template>
    <figure class="bg-white">
        <img class="rounded-t-lg" :src="image" alt="image maison">
        <figcaption class="px-5 py-7 border-2 border-t-0 rounded-b-lg">
            <div class="flex flex-col gap-2">
                <div class="flex flex-wrap gap-1 items-center">
                    <p class="text-indigo-500 text-2xl font-bold font-inter">${{prix}}</p>
                    <p class="text-gray-500 font-inter text-base">/month</p>
                    <div><IconCoeur class="ml-24" :class="{ 'fill-red-300': préféré }"></IconCoeur></div>
                </div>
                <h3 class="flex-center font-inter text-2xl font-semibold text-gray-900">{{nom}}</h3>
                <p class="flex flex-end font-inter text-gray-500 text-base">{{adresse}}</p>
            </div>
            <hr class="border-indigo-100 border-t-2 my-2"/>
            <div class="flex flex-wrap justify-between text-sm">
                <div><IconBed class="inline-block align-top" />{{bed}}</div>
                <div><IconBath class="inline-block align-top"></IconBath> {{bath}}</div>
                <div><IconSize class="inline-block align-top"></IconSize>{{size}}</div>
            </div>
        </figcaption>
    </figure>
</template>

<script setup >
import IconBed   from "./icones/bath.vue"
import IconBath  from "./icones/bath.vue" 
import IconSize  from "./icones/size.vue"
import IconCoeur from "./icones/coeur.vue"

    defineProps:{
        prix= Number,
        nom= String,
        image= String,
        préféré= Boolean,
        adresse= String,
        bed= String,
        bath= String,
        size= String,
    },
</script>

