<template>
    <section class="films">
        <div class="container">
            <h1 class="films-title">ТОП ФИЛЬМОВ</h1>
            <div class="btns-wrapper" :class="{ hide: !this.pageIsVisible }">
                <button class="top" @click="prevPage">Предыдущая страница</button>
                <p class="pageCounter"> {{this.page}} </p>
                <button class="top" @click="nextPage">Следующая страница</button>
            </div>
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
        page: {type: Number},
        pageIsVisible: {type: Boolean},
    },
    components: {
        FilmCard,
    },
    methods: {
        showModal(film) {
            this.$emit('show-modal', film)
        },
        prevPage() {
            this.$emit('prev-page')
        },
        nextPage() {
            this.$emit('next-page')
        },
    }
}
</script>

<style scoped>
.btns-wrapper.hide {
    display: none;
}
.pageCounter {
    margin: 0 10px;
    font-size: 20px;
}
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.btns-wrapper {
    margin: 15px 0;
    display: flex;
    align-items: center;
}
.films {
    min-height: calc(100vh - 50px);
    background-color: rgba(143, 0, 255, 0.15);
    padding: 20px 0;
}
.top {
    padding: 5px 15px;
    margin: 0;
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
