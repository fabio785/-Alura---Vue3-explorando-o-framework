<template>
    <BoxComp>
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column">
                <CronometroTarefa :tempoEmSegundos="tarefa.duracaoEmSegundos"/>
            </div>
        </div>
    </BoxComp>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import CronometroTarefa from './CronometroTarefa.vue'
import ITarefa from '@/interfaces/ITarefa';
import BoxComp from './BoxComp.vue';

export default defineComponent({
    name:'TarefaItem',
    components:{
        CronometroTarefa,
        BoxComp
    },
    props:{
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true
        }
    }
})
</script>

<style scoped>
    .box{
        background-color: #FAF0CA;
    }
</style>