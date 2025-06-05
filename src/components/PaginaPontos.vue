<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination } from 'swiper/modules';

import 'swiper/css';
import 'swiper/css/pagination';
import { tarefasDiarias } from '@/tarefas/tarefasDiarias';
import { tarefasPlastico } from '@/tarefas/tarefasPlastico';
import { tarefasMetal } from '@/tarefas/tarefasMetal';
import { tarefasPapel } from '@/tarefas/tarefasPapel';
import { tarefasVidro } from '@/tarefas/tarefasVidro';

export default {
    components: {
        Swiper,
        SwiperSlide,
    },
    data() {
        return {
            pagination: Pagination,
            tarefasDiarias,
            tarefasPlastico,
            tarefasMetal,
            tarefasPapel,
            tarefasVidro,
            breakpoints: {
                1024: {
                    slidesPerView: 3,
                },
                1450: {
                    slidesPerView: 4,
                }
            }
        };
    },
}
</script>

<template>
    <section class="missoes">
        <h1 class="titulo-missao">--missões diárias--</h1>
        <Swiper :modules="[pagination]" :spaceBetween="10" :slidesPerView="1" :pagination="{ clickable: true }" :breakpoints="breakpoints">
            <div class="swiper-pagination" style="position: initial; padding: 1em;"></div>
            <SwiperSlide v-for="tarefaDiaria in tarefasDiarias" :key="tarefaDiaria.tipo">
                <div class="card-missao" :class="tarefaDiaria.tipo">
                    <div class="card-imagem">
                        <img src="../assets/images/tarefas/tarefa-tudo.png" alt="">
                    </div>
                    <hr />
                    <div class="card-info">
                        <h3 class="card-titulo">{{ tarefaDiaria.titulo }}</h3>
                        <p class="card-descricao">{{ tarefaDiaria.descricao }}</p>
                        <h3 class="card-pontos">Pontos: {{ tarefaDiaria.pontos }}</h3>
                    </div>
                    <button class="concluir-tarefa-botao">Pronto</button>
                </div>
            </SwiperSlide>
        </Swiper>
    </section>

    <section class="missoes">
        <h1 class="titulo-missao">--plásticos--</h1>
        <Swiper :modules="[pagination]" :spaceBetween="10" :slidesPerView="1" :pagination="{ clickable: true }"  :breakpoints="breakpoints">
            <div class="swiper-pagination" style="position: initial; padding: 1em;"></div>
            <SwiperSlide v-for="tarefaPlastico in tarefasPlastico" :key="tarefaPlastico.tipo">
                <div class="card-missao" :class="tarefaPlastico.tipo">
                    <div class="card-imagem">
                        <img src="../assets/images/tarefas/tarefa-plastico.png" alt="">
                    </div>
                    <hr />
                    <div class="card-info">
                        <h3 class="card-titulo">{{ tarefaPlastico.titulo }}</h3>
                        <p class="card-descricao">{{ tarefaPlastico.descricao }}</p>
                        <h3 class="card-pontos">Pontos: {{ tarefaPlastico.pontos }}</h3>
                    </div>
                    <button class="concluir-tarefa-botao">Pronto</button>
                </div>
            </SwiperSlide>
        </Swiper>
    </section>

    <section class="missoes">
        <h1 class="titulo-missao">--metais--</h1>
        <Swiper :modules="[pagination]" :spaceBetween="10" :slidesPerView="1" :pagination="{ clickable: true }"
            :breakpoints="breakpoints">
            <div class="swiper-pagination" style="position: initial; padding: 1em;"></div>
            <SwiperSlide v-for="tarefaMetal in tarefasMetal" :key="tarefaMetal.tipo">
                <div class="card-missao" :class="tarefaMetal.tipo">
                    <div class="card-imagem">
                        <img src="../assets/images/tarefas/tarefa-metal.png" alt="">
                    </div>
                    <hr />
                    <div class="card-info">
                        <h3 class="card-titulo">{{ tarefaMetal.titulo }}</h3>
                        <p class="card-descricao">{{ tarefaMetal.descricao }}</p>
                        <h3 class="card-pontos">Pontos: {{ tarefaMetal.pontos }}</h3>
                    </div>
                    <button class="concluir-tarefa-botao">Pronto</button>
                </div>
            </SwiperSlide>
        </Swiper>
    </section>

    <section class="missoes">
        <h1 class="titulo-missao">--papéis--</h1>
        <Swiper :modules="[pagination]" :spaceBetween="10" :slidesPerView="1" :pagination="{ clickable: true }" :breakpoints="breakpoints">
            <div class="swiper-pagination" style="position: initial; padding: 1em;"></div>
            <SwiperSlide v-for="tarefaPapel in tarefasPapel" :key="tarefaPapel.tipo">
                <div class="card-missao" :class="tarefaPapel.tipo">
                    <div class="card-imagem">
                        <img src="../assets/images/tarefas/tarefa-papel.png" alt="">
                    </div>
                    <hr />
                    <div class="card-info">
                        <h3 class="card-titulo">{{ tarefaPapel.titulo }}</h3>
                        <p class="card-descricao">{{ tarefaPapel.descricao }}</p>
                        <h3 class="card-pontos">Pontos: {{ tarefaPapel.pontos }}</h3>
                    </div>
                    <button class="concluir-tarefa-botao">Pronto</button>
                </div>
            </SwiperSlide>
        </Swiper>
    </section>

    <section class="missoes">
        <h1 class="titulo-missao">--vidros--</h1>
        <Swiper :modules="[pagination]" :spaceBetween="10" :slidesPerView="1" :pagination="{ clickable: true }" :breakpoints="breakpoints">
            <div class="swiper-pagination" style="position: initial; padding: 1em;"></div>
            <SwiperSlide v-for="tarefaVidro in tarefasVidro" :key="tarefaVidro.tipo">
                <div class="card-missao" :class="tarefaVidro.tipo">
                    <div class="card-imagem">
                        <img src="../assets/images/tarefas/tarefa-vidro.png" alt="">
                    </div>
                    <hr />
                    <div class="card-info">
                        <h3 class="card-titulo">{{ tarefaVidro.titulo }}</h3>
                        <p class="card-descricao">{{ tarefaVidro.descricao }}</p>
                        <h3 class="card-pontos">Pontos: {{ tarefaVidro.pontos }}</h3>
                    </div>
                    <button class="concluir-tarefa-botao">Pronto</button>
                </div>
            </SwiperSlide>
        </Swiper>
    </section>
</template>

<style>
.swiper {
    z-index: 0;
    width: 100%;
}

.swiper-slide {
    display: flex;
    align-items: center;
    justify-content: center;
}

.swiper-pagination-bullet {
    background-color: var(--branco) !important;
}

.swiper-pagination-bullet-active {
    background-color: var(--verde-titulo) !important;
}

.missoes {
    display: flex;
    flex-direction: column;
    align-items: center;

}

.titulo-missao {
    width: 100%;
    color: var(--verde-titulo);
    background-color: var(--cinza);
    padding: 1em;
    margin: 1em;
    font-family: var(--font-retro);
    font-size: 14px;
    font-weight: normal;
}

.card-missao {
    height: 100%;
    border-top: 1.5em solid;
    background-color: var(--cinza);
    width: 250px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.card-imagem {
    width: 100%;
    text-align: center;
}

hr {
    width: 100%;
}

.card-imagem {
    padding: 1em;
}

.card-info {
    text-align: center;
    color: black;
    color: var(--branco);
    font-family: var(--font-padrao);
    padding: 1em;
}

.card-titulo {
    font-family: var(--font-retro);
    font-size: 13px;
    font-weight: normal;
}

.card-descricao {
    font-size: 13px;
    padding: 1em 0;
}

.card-pontos {
    font-family: var(--font-retro);
    font-size: 12px;
    font-weight: normal;
}

.concluir-tarefa-botao {
    width: 100%;
    padding: .8em 1em;
    margin-top: 1em;
    font-family: var(--font-retro);
    color: var(--branco);
    border: none;
}

/* CARDS TAREFAS PERSONALIZADOS */
.tarefa-tudo .concluir-tarefa-botao {
    background-color: var(--roxo);
}

.tarefa-tudo,
.tarefa-tudo hr,
.tarefa-tudo .concluir-tarefa-botao {
    border-color: var(--roxo);
}

.tarefa-tudo .card-imagem {
    background-color: #8558ff;
}

.tarefa-plastico .concluir-tarefa-botao {
    background-color: var(--vermelho);
}

.tarefa-plastico,
.tarefa-plastico hr,
.tarefa-plastico .concluir-tarefa-botao {
    border-color: var(--vermelho);
}

.tarefa-plastico .card-imagem {
    background-color: #ff5596c4;
}

.tarefa-metal .concluir-tarefa-botao {
    background-color: var(--amarelo);
}

.tarefa-metal,
.tarefa-metal hr,
.tarefa-metal .concluir-tarefa-botao {
    border-color: var(--amarelo);
}

.tarefa-metal .card-imagem {
    background-color: #ffd966c4;
}

.tarefa-papel .concluir-tarefa-botao {
    background-color: var(--azul);
}

.tarefa-papel,
.tarefa-papel hr,
.tarefa-papel .concluir-tarefa-botao {
    border-color: var(--azul);
}

.tarefa-papel .card-imagem {
    background-color: #5eb3ffc4;
}

.tarefa-vidro .concluir-tarefa-botao {
    background-color: var(--verde);
}

.tarefa-vidro,
.tarefa-vidro hr,
.tarefa-vidro .concluir-tarefa-botao {
    border-color: var(--verde);
}

.tarefa-vidro .card-imagem {
    background-color: #70e7a2c4;
}
</style>