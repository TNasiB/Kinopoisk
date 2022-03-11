<template>
    <div class="film-card flex-column" :style="cssDefine" @click="show">
        <p class="film-name">{{ film.nameRu }}</p>
        <p class="film-rating">🌟{{ film.rating }}</p>
    </div>
</template>

<script>

export default {
    name: 'FilmCard',
    props: {
        film: {type: Object},
    },
    computed: {
        cssDefine() {
            return {
                '--imageFilm': `url(${this.film.posterUrlPreview})`
            }
        },
    },
    methods: {
        show() {
            this.$emit('show-modal', this.film)
            this.$modal.show('modal-film')
        },
    }
}
</script>

<style scoped>
.film-rating {
    z-index: 10;
    color: #fff;
    font-size: 30px;
}
.film-card {
    cursor: pointer;
    position: relative;
    min-width: 200px;
    flex: 1;
    height: 400px;
    background-image: var(--imageFilm);
    background-repeat: no-repeat;
    background-size: 290px;
    padding: 5px;
    margin: 10px;
    background-position: center;
    justify-content: space-between;
    align-items: center;
    text-align: center;    
    transition: background-size .2s;
}
.film-card:hover {
    background-size: 330px;
}
.film-card::before {
    position: absolute;
    content: '';
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.4);
}
.film-card:hover::before {
    background-color: rgba(0, 0, 0, 0.2);
}
.film-name {
    color: #fff;
    align-self: flex-start;
    text-align: center;
    font-size: 20px;
    z-index: 2;
    margin-top: 10px;
    width: 100%;
}
</style>