<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroTeste :tempoEmSegundos="tempoEmSegundos" />
        <button class="button" @click="iniciar" :disabled="cronomeroRodando">
            <span class="icon">
                <i class="fas fa-play"></i>
            </span>
            <span>play</span>
        </button>
        <button class="button" @click="finalizar" :disabled="!cronomeroRodando">
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span>
            <span>stop</span>
        </button>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CronometroTeste from "./CronometroTeste.vue";

export default defineComponent({
    name: "TemporizadorTeste",
    emits: ["aoTemporizadorFinalizado"],
    components: {
        CronometroTeste
    },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronomeroRodando: false
        };
    },
   
    methods: {
        iniciar() {
            this.cronomeroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1;
            }, 1000);
        },
        finalizar() {
            this.cronomeroRodando = false
            clearInterval(this.cronometro)
            this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        },
    },
});
</script>