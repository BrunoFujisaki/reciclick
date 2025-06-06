<script>
import { pontos } from '@/pontos-reciclagem/pontos';
import L from 'leaflet';
import 'leaflet/dist/leaflet.css';

export default {
  data() {
    return {
      map: null,
      marcador: null,
      marcadores: [],
      filtroSelecionado: '',
      filtros: [
        { nome: 'Tudo', tipo: 'Tudo', cor: 'btn-tudo' },
        { nome: 'Metal', tipo: 'metal', cor: 'btn-metal' },
        { nome: 'Vidro', tipo: 'vidro', cor: 'btn-vidro' },
        { nome: 'Papel', tipo: 'papel', cor: 'btn-papel' },
        { nome: 'Plástico', tipo: 'plastico', cor: 'btn-plastico' }
      ],
      pontos,
      icones: {
        metal: L.icon({ iconUrl: 'metal.png', iconAnchor: [10, 30], popupAnchor: [0, -40] }),
        vidro: L.icon({ iconUrl: 'vidro.png', iconAnchor: [10, 30], popupAnchor: [0, -40] }),
        papel: L.icon({ iconUrl: 'papel.png', iconAnchor: [10, 30], popupAnchor: [0, -40] }),
        plastico: L.icon({ iconUrl: 'plastico.png', iconAnchor: [10, 30], popupAnchor: [0, -40] }),
      },
      cep: ''
    };
  },
  methods: {
    inicializarMapa() {
      // Inicializa o mapa e salva no this.map
      this.map = L.map('map', { zoomControl: false }).setView([-23.4273, -51.9375], 16);

      // Adiciona camada de mapa
      L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
        ext: 'png'
      }).addTo(this.map);
    },

    selecionarFiltro(filtro) {

      if (this.filtroSelecionado == filtro) {
        this.filtroSelecionado = '';
        this.marcadores.forEach(m => this.map.removeLayer(m));
        this.marcadores = [];

      } else {
        this.filtroSelecionado = filtro;

        const pontosFiltrados = filtro === 'Tudo'
          ? this.pontos
          : this.pontos.filter(ponto => ponto.tipo === filtro);

        this.marcadores.forEach(m => this.map.removeLayer(m));
        this.marcadores = [];


        pontosFiltrados.forEach(ponto => {
          const marcador = L.marker([ponto.lat, ponto.lng], { icon: this.icones[ponto.tipo] })
            .addTo(this.map)
            .bindPopup(`<b>${ponto.nome}</b><br>Coleta de ${ponto.tipo}`);
          this.marcadores.push(marcador);
        });
      }
    },

    async buscarCep() {
      if (!this.cep) {
        alert('Digite um CEP!');
        return;
      }

      try {
        // 🔍 Consulta ViaCEP para transformar o CEP em endereço
        const viaCepResponse = await fetch(`https://viacep.com.br/ws/${this.cep}/json/`);
        const viaCepData = await viaCepResponse.json();

        if (viaCepData.erro) {
          alert('CEP não encontrado no ViaCEP!');
          return;
        }

        const endereco = `${viaCepData.logradouro}, ${viaCepData.bairro}, ${viaCepData.localidade}, ${viaCepData.uf}, Brasil`;

        // 🌍 Consulta Nominatim para obter as coordenadas
        const geocodeResponse = await fetch(
          `https://nominatim.openstreetmap.org/search?format=json&q=${encodeURIComponent(endereco)}`
        );

        const geocodeData = await geocodeResponse.json();

        if (geocodeData.length === 0) {
          alert('Não foi possível encontrar as coordenadas!');
          return;
        }

        const lat = parseFloat(geocodeData[0].lat);
        const lon = parseFloat(geocodeData[0].lon);
        const displayName = geocodeData[0].display_name;

        // 🔄 Centraliza o mapa
        this.map.setView([lat, lon], 16);

        if (this.marcador) {
          this.map.removeLayer(this.marcador);
        }

        this.marcador = L.marker([lat, lon])
          .addTo(this.map)
          .bindPopup(`<b>Local encontrado:</b><br>${displayName}`)
          .openPopup();
      } catch (error) {
        console.error('Erro:', error);
        alert('Ocorreu um erro ao buscar o CEP.');
      }
    }

  },

  mounted() {
    this.inicializarMapa();
  }

};
</script>

<template>
  <section class="interface-mapa">
    <div id="map"></div>

    <div class="menu-inferior">
      <div class="input-container">
          <input v-model="cep" type="text" class="input-cep" placeholder="Informe o CEP">
          <button @click="buscarCep" class="input-botao">
            <img src="../assets/images/search.png" alt="">
          </button>
      </div>
      <ul class="lista-reciclaveis">
        <li class="lista-reciclaveis-item" v-for="filtro in filtros" :key="filtro.tipo">
          <button :class="[{ selecionado: filtroSelecionado === filtro.tipo }, filtro.cor]"
            @click="selecionarFiltro(filtro.tipo)">
            {{ filtro.nome }}
          </button>
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>

.interface-mapa {
  position: relative;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.input-container {
  width: 65%;
  padding: .5em;
  border-radius: 8px;
  background: #3d3d3d;
  border: 1px solid white;
  z-index: 1;
  position: relative;
  padding-left: 3em;
}

.input-cep {
  width: 100%;
  border: none;
  color: var(--branco);
  background: transparent;
  outline: none;
  font-size: 16px;
}

.input-botao {
  position: absolute;
  left: 10px;
  top: 4px;
  background-color: transparent;
  border: none;
}

.input-cep::placeholder {
  font-family: var(--font-padrao);
  font-size: 16px;
  font-weight: normal;
  /* padding-left: 2em; */
  color: var(--branco);
}

#map {
  height: 100vh;
  width: 100%;
  z-index: 0;
}

.menu-inferior {
  position: fixed;
  width: 100%;
  bottom: 0;
  background-color: #0000009a;
  backdrop-filter: blur(40px);
  -webkit-backdrop-filter: blur(40px);
  display: flex;
  flex-direction: column;
  padding: 3em 0 3em 0;
  align-items: center;
  gap: 2em;
}

.lista-reciclaveis {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  gap: 1em;
}

.lista-reciclaveis-item button {
  padding: 1em;
  border: none;
  font-family: var(--font-retro);
  font-size: 15px;
  border-radius: 8px;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.btn-papel {
  background-color: #0077ff49;

}

.btn-plastico {
  background-color: #ff006254;
}

.btn-vidro {
  background-color: #00dfa441;
}

.btn-metal {
  background-color: #ffd65a49;
}

.btn-tudo {
  background-color: #4400ff3f;
}

.btn-metal.selecionado {
  background-color: var(--amarelo);
  color: #fff;
}

.btn-vidro.selecionado {
  background-color: var(--verde);
  color: #fff;
}

.btn-papel.selecionado {
  background-color: var(--azul);
  color: #fff;
}

.btn-plastico.selecionado {
  background-color: var(--vermelho);
  color: #fff;
}

.btn-tudo.selecionado {
  background-color: var(--roxo);
  color: #fff;
}
</style>