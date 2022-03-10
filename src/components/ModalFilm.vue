<template>
    <modal class="modal-film" name="modal-film">
        <div class="modal-wrapper flex">
            <div class="film-img" :style="cssDefine"></div>
            <div class="film-inf">
                <p class="film-name">{{ film.nameRu }}</p>
                <p class="film-desc">{{ film.description }}</p>
                <p class="film-year"> Год создания: {{ film.year }} </p>
                <p class="film-rating">Рейтинг: {{ film.rating }} </p>
                <button class="film-modal-close" @click.prevent="hide">Закрыть</button>
            </div>
        </div>
    </modal>
</template>

<script>
export default {
    name: 'ModalFilm',
    props: {
        film: {type: Object}
    },
    methods: {
        hide() {
            this.$modal.hide('modal-film')
        }
    },
    mount() {
        this.show()
    },
    computed: {
        cssDefine() {
            return {
                '--imageFilm': `url(${this.film.posterUrlPreview})`
            }
        },
    },
}
</script>

<style>
.film-modal-close {
    padding: 5px;
    background-color: #8f00ff;
    border-radius: 5px;
    border: none;
    color: #fff;
    font-size: 25px;
}
.film-rating {
    margin: 20px 0;
}
.film-year {
    margin-top: 20px;
    font-family: sans-serif;
}
.film-desc {
    font-size: 12px;
    font-family: sans-serif;
    margin-top: 10px;
}
.vm--modal {
    height: 50vh !important;
}
.modal-film {
    display: flex;
}
.film-inf {
    padding: 12px;
    width: 60%;
    font-weight: 40;
    display: flex;
    overflow: auto;
    flex-direction: column;
    justify-content: space-around;
}
.film-name {
    font-size: 20px;
    text-align: center;
}
.modal-wrapper {
    height: 100%;
}
.film-img {
    width: 40%;
    background-image: var(--imageFilm);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    height: 100%;
}
</style>
