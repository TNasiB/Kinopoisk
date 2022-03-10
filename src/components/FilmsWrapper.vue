<template>
    <section class="films">
        <div class="container">
            <h1 class="films-title">Топ 20 фильмов</h1>
            <div class="films-inner">
                <FilmCard v-for="(film, index) in films" :key="index" :film="film" @show-modal="showModal"/>
            </div>
        </div>
    </section>
</template>

<script>
import FilmCard from './FilmCard'
export default {
    name: 'FilmsWrapper',
    props: {
        films: {type: Array},
        film: {type: Object},
    },
    components: {
        FilmCard,
    },
    methods: {
        showModal(film) {
            this.$emit('show-modal', film)
        },
    }
}
</script>

<style scoped>
.films {
    min-height: calc(100vh - 50px);
    background-color: rgba(143, 0, 255, 0.15);
    padding: 20px 0;
}
.films-inner {
    display: flex;
    flex-wrap: wrap;
}
.films-title {
    font-size: 30px;
    color: #000;
    margin-left: 10px;
    text-align: center;
    margin-bottom: 10px;
}
</style>
