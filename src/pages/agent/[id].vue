<script setup lang="ts">
    import FormulaireAgent from "../../components/FormulaireAgent.vue";
    const props = defineProps<{
      id: String;
    }>();

    
    </script>
    <template>
      <div class="p-2">
        <FormulaireAgent :id="id" />
        
      </div>
    </template>