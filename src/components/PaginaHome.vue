<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination } from 'swiper/modules';

import 'swiper/css';
import 'swiper/css/pagination';

export default {
    components: {
        Swiper,
        SwiperSlide,
    },
    data() {
        return {
            pagination: Pagination,
        };
    },
};
</script>

<template>
    <h1>CONTEUDO PRINCIPAL</h1>
<!-- Carrossel se quiser utilizar
    <Swiper :modules="[pagination]" :spaceBetween="30" :slidesPerView="1" :pagination="{ clickable: true }">
        <SwiperSlide>
            conteudo aqui
        </SwiperSlide>
        <SwiperSlide>
            conteudo aqui
        </SwiperSlide>
        <SwiperSlide>
            conteudo aqui
        </SwiperSlide>
    </Swiper> 
-->

</template>

<style scoped>
.swiper {
    z-index: 0;
    width: 100%;
    height: 100%;
}

/* .swiper-slide {
    background-color: var(--azul);
    font-family: var(--font-padrao);
    color: var(--branco);
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
} */

.swiper-slide img {
    width: 100%;
}

.swiper-pagination-bullet {
    background: blue;
}

.swiper-pagination-bullet-active {
    background: red;
}
</style>