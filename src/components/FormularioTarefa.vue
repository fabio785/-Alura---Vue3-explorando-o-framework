<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column i-8" role="form" aria-label="Formulário para criação de uma nova tarefa" >
                <input type="text" class="input" v-model="descricao" placeholder="Qual tarefa você deseja iniciar?"/>
            </div>
            <div class="column">
                <TemporizadorTarefa @aoTemporizadorFinalizado="finalizarTarefa"/>
                
            </div>
        </div>
    </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import TemporizadorTarefa from './TemporizadorTarefa.vue'

export default defineComponent({
    name: 'FormularioTarefa',
    emits:['aoSalvarTarefa'],
    data() {
        return{
            descricao:''
        }
    },
    components:{
        TemporizadorTarefa
    },
    methods:{
        finalizarTarefa(tempoDecorrido: number) : void{
            this.$emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao
            });
            this.descricao = ''
        }
    }
});
</script>
<style>
.formulario{
    color:var(--texto-primario);
    background-color: var(--bg-primario);
}
</style>