<template>
    <div class="box has-text-weight-bold">
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao}}
            </div>
            <div class="column">
                <CronometroTarefa :tempoEmSegundos="tarefa.duracaoEmSegundos"/>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import CronometroTarefa from './CronometroTarefa.vue'
import ITarefa from '@/interfaces/ITarefa';

export default defineComponent({
    name:'TarefaItem',
    components:{
        CronometroTarefa
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