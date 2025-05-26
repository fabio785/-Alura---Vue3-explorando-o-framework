<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro' : modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema"></BarraLateral>
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioTarefa @aoSalvarTarefa="salvarTarefa" ></FormularioTarefa>
      <div class="lista">
        <TarefaItem v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
        <BoxComp v-if="listaEstaVazia">
          Você não está muito produtivo hoje :(
        </BoxComp>
      </div>     
    </div>

  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import FormularioTarefa from './components/FormularioTarefa.vue';
import TarefaItem from './components/TarefaItem.vue';
import BoxComp from './components/BoxComp.vue';
import ITarefa from './interfaces/ITarefa';

export default defineComponent({
  name: 'App',
  components: { 
    BarraLateral,
    FormularioTarefa,
    TarefaItem,
    BoxComp
  },
  data() {
    return {
      tarefas:[] as ITarefa[], 
      modoEscuroAtivo: false
    }
  },
  computed:{
    listaEstaVazia() : boolean{
      return this.tarefas.length === 0;
    }
  },
  methods:{
    salvarTarefa(tarefa: ITarefa){
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo: boolean){
      this.modoEscuroAtivo = modoEscuroAtivo;
    }
  }
});
</script>

<style>
.lista{
  padding: 1.25rem;
}

main{
  --bg-primario:#fff;
  --texto-primario:#000;
}
main.modo-escuro{
  --bg-primario:#2b2d42;
  --texto-primario:#ddd;
}

.conteudo{
  background-color: var(--bg-primario);
  color: var(--texto-primario);
}
</style>
