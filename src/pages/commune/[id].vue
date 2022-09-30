<script setup lang="ts">
    import FormulaireCommune from "../../components/FormulaireCommune.vue";
    const props = defineProps<{
      id: String;
    }>();

    
    </script>
    <template>
      <div class="p-2">
        <FormulaireCommune :id="id" />
        
      </div>
    </template>