<template>
    <section class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoEmSegundos="tempoEmSegundos" />
        <Botao @clicado="iniciar" icone="fas fa-play" texto="play" :desabilitado="cronometroRodando" />
        <Botao @clicado="finalizar" icone="fas fa-stop" texto="stop" :desabilitado="!cronometroRodando" />
        <!-- <Botao @clicado="zerar" icone="fas fa-stopwatch" texto="zerar" :desabilitado="!zerarCronometro" /> -->
    </section>
</template>


<script lang="ts">
import { defineComponent } from 'vue';
import Cronometro from './Cronometro.vue';
import Botao from './Botao.vue';


export default defineComponent({

    name: "Temporizador",
    emits: ["aoTemporizadorFinalizado"],
    components: {
        Cronometro,
        Botao
    },

    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false,
            zerarCronometro: false
        }
    },

    methods: {
        iniciar() {
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1;
                this.cronometroRodando = true;
                this.zerarCronometro = true;
            }, 1000);
        },
        finalizar() {
            this.cronometroRodando = false;
            clearInterval(this.cronometro);
            this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos)
            this.tempoEmSegundos = 0;
        },
        zerar() {
            this.zerarCronometro = false;
            this.tempoEmSegundos = 0;
            this.cronometroRodando = false;
        }
    }
});
</script>