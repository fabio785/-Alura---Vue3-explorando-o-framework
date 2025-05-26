<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroTarefa :tempoEmSegundos="tempoEmSegundos"/>
        <!-- <button class="button" @click="iniciar" :disabled="cronometroRodando">
            <span class="icon">
                <i class="fas fa-play"></i>
            </span>
            <span>play</span>
        </button> -->
        <!-- <button class="button" @click="finalizar" :disabled="!cronometroRodando">
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span>
            <span>stop</span>
        </button> -->

        <BotaoComp @clicado="iniciar" icone="fas fa-play" texto="play" :desabilitado="cronometroRodando" />

        <BotaoComp @clicado="finalizar" icone="fas fa-stop" texto="stop" :desabilitado="!cronometroRodando" />
    </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import CronometroTarefa from './CronometroTarefa.vue'
import BotaoComp from './BotaoComp.vue'

export default defineComponent({
    name: 'TemporizadorTarefa',
    emits:['aoTemporizadorFinalizado'],
    components:{
        CronometroTarefa,
        BotaoComp
    },
    data () {
        return {
            tempoEmSegundos: 0,
            cronometro:0, 
            cronometroRodando:false
        };
    },
    
    methods: {
        iniciar () {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1; 
            }, 1000);
        },
        finalizar () {
            this.cronometroRodando = false
            clearInterval(this.cronometro);
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        },
    },
});

</script>