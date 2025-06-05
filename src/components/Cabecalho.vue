<script>
export default {
    data() {
        return {
            menuVisivel: false,
            mostrarTelaUsuario: false
        }
    },
    methods: {
        toggleMenu() {
            this.menuVisivel = !this.menuVisivel;
        },

        toggleTelaUsuario() {
            this.mostrarTelaUsuario = !this.mostrarTelaUsuario;
        },
        cliqueFora(event) {
            const menu = this.$refs.menu;
            if (this.menuVisivel && menu && !menu.contains(event.target)) {
                this.toggleMenu();
            }
        }
    },
    emits: ['pagina'],
    props: {
        paginaAtual: String
    },
    mounted() {
        document.addEventListener('click', this.cliqueFora);
    },
    beforeUnmount() {
        document.removeEventListener('click', this.cliqueFora);
    }
}
</script>

<template>
    <header class="cabecalho">
        <div class="container">
            <button class="menu" @click.stop="toggleMenu">
                <img src="../assets/images/menu.png" alt="">
            </button>
            <transition name="slide-left">
                <ul v-if="menuVisivel" class="menu-lista" ref="menu">
                    <li class="menu-lista-item">
                        <button @click.stop="toggleMenu">
                            <img src="../assets/images/fechar.png" alt="">
                        </button>
                    </li>
                    <li class="menu-lista-item">
                        <a href="#" class="lista-item-link" @click="$emit('pagina', 'home')"
                            :class="{ ativo: paginaAtual === 'home' }">
                            Home
                        </a>
                    </li>

                    <li class="menu-lista-item">
                        <a href="#" class="lista-item-link" @click="$emit('pagina', 'pontos')"
                            :class="{ ativo: paginaAtual === 'pontos' }">
                            Pontos
                        </a>
                    </li>

                    <li class="menu-lista-item">
                        <a href="#" class="lista-item-link" @click="$emit('pagina', 'mapa')"
                            :class="{ ativo: paginaAtual === 'mapa' }">
                            Mapa
                        </a>
                    </li>
                </ul>
            </transition>
            <h1 class="titulo">--reciclick--</h1>
        </div>
        <button class="usuario" @click="toggleTelaUsuario()">
            <img src="../assets/images/usuario.png" alt="">
        </button>
        <!-- Tela que sobe -->
        <transition name="slide-up">
            <div v-if="mostrarTelaUsuario" class="tela-usuario">
                <button class="fechar" @click="toggleTelaUsuario">
                    <img src="../assets/images/fechar.png" alt="">
                </button>
                <!-- conteúdo da tela aqui -->
                <h1 class="tela-usuario-titulo">Ranking Atual</h1>
            </div>
        </transition>
    </header>
</template>

<style scoped>
/* Transição deslizando da esquerda */
.slide-left-enter-active,
.slide-left-leave-active {
    transition: transform 0.3s ease;
}

.slide-left-enter-from {
    transform: translateX(-100%);
}

.slide-left-enter-to {
    transform: translateX(0);
}

.slide-left-leave-from {
    transform: translateX(0);
}

.slide-left-leave-to {
    transform: translateX(-100%);
}

/* Animação slide para cima (tela usuário) */
.slide-up-enter-active,
.slide-up-leave-active {
    transition: all 0.5s ease;
}

.slide-up-enter-from {
    transform: translateY(100%);
    opacity: 0;
}

.slide-up-enter-to {
    transform: translateY(0);
    opacity: 1;
}

.slide-up-leave-from {
    transform: translateY(0);
    opacity: 1;
}

.slide-up-leave-to {
    transform: translateY(100%);
    opacity: 0;
}

/* Estilo da tela que sobe */
.tela-usuario {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100vw;
    height: 93vh;
    background-color: #0000009a;
    backdrop-filter: blur(40px);
    -webkit-backdrop-filter: blur(40px);
    z-index: 3;
    padding: 1em;
    box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.3);
    font-family: var(--font-padrao);
    overflow-y: auto;
}

.tela-usuario-titulo {
    padding: 1em 0;
    font-family: var(--font-retro);
    font-weight: normal;
    font-size: 18px
}

.tela-usuario .fechar {
    background-color: transparent;
    border: none;
}

.inputs {
    display: flex;
    flex-direction: column;
    gap: 1em;
    margin-top: 3em;
}

.inputs label {
    display: flex;
    align-items: center;
}

.usuario-input {
    font-family: var(--font-padrao);
    border: none;
    background-color: transparent;
    color: var(--branco);
    font-size: 16px;
}

.usuario-input::placeholder {
    color: var(--branco);
}

.cabecalho {
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: relative;
    background-color: var(--cinza);
}

.container {
    display: flex;
    align-items: center;
}

.cabecalho .titulo {
    font-family: var(--font-retro);
    color: var(--verde-titulo);
    font-size: 16px;
    font-weight: normal;
}

.menu {
    background-color: transparent;
    border: none;
    cursor: pointer;
}

.usuario {
    background-color: transparent;
    border: none;
}

.menu,
.usuario {
    margin: 1em;
}

.menu-lista {
    position: fixed;
    top: 0;
    background-color: #0000009a;
    backdrop-filter: blur(40px);
    -webkit-backdrop-filter: blur(40px);
    width: 45vw;
    padding-top: 1em;
    height: 100vh;
    z-index: 2;
}

.menu-lista-item button {
    background-color: transparent;
    border: none;
}

.lista-item-link.ativo {
    color: var(--verde);
    border-bottom: 4px solid var(--verde);
    position: relative;
    width: max-content;
}

.lista-item-link {
    position: relative;
    text-transform: uppercase;
    font-family: var(--font-retro);
    color: var(--verde-titulo);
    text-decoration: none;
    font-weight: 500;
    font-size: 16px;
}

.lista-item-close {
    padding: .5em;
}

.menu-lista-item {
    padding: 1em;
}
</style>