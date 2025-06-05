<script>
import 'leaflet/dist/leaflet.css';
import Cabecalho from './components/Cabecalho.vue';
import PaginaMapa from './components/PaginaMapa.vue';
import PaginaHome from './components/PaginaHome.vue';
import PaginaPontos from './components/PaginaPontos.vue';

export default {
  components: { Cabecalho, PaginaHome, PaginaMapa, PaginaPontos},
  data() {
    return {
      paginaAtual: 'home'
    }
  },
  methods: {
    mudarPagina(pagina) {
      this.paginaAtual = pagina
    }
  }
}
</script>
<template>
      <Cabecalho :pagina-atual="paginaAtual" @pagina="mudarPagina" />
      <PaginaHome v-if="paginaAtual == 'home'" />
      <PaginaMapa v-if="paginaAtual == 'mapa'" />
      <PaginaPontos v-if="paginaAtual == 'pontos'" />
    
    <!-- <div class="rodape">
      <Rodape />
    </div> -->
</template>
<style scoped>
/* .pagina {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.conteudo {
  flex: 1;
} */
</style>