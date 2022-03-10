<template>
    <header>
        <div class="container">
            <div class="header__wrapper">
                <span class="header__logo">Кинопоиск на минималках</span>
                <div class="setting-wrapper flex">
                    <button @click="sortFilms" class="top">Сортировать по рейтингу</button>
                    <button @click="getFilms" class="top">ТОП 20</button>
                    <SearchInput @send-query="showQuery"/>
                </div>
            </div>
        </div>
    </header>
</template>

<script>
import SearchInput from "./SearchInput"
export default {
    name: "HeaderComp",
    components: {
        SearchInput,
    },
    methods: {
        showQuery(query) {
            this.$emit('send-query', query)
        },
        getFilms() {
            this.$emit('get-films')
            let titleSite = document.querySelector(".films-title")
            titleSite.textContent = `Топ 20 фильмов`

        },
        sortFilms() {
            this.$emit('sort-films')
        }
    }
}
</script>

<style scoped>
header {
    color: #fff;
    background-color: #8F00FF;
}
.header__logo {
    font-size: 30px;
    font-weight: 700;
}
.top {
    background: #fff;
    border: none;
    margin-right: 10px;
    border-radius: 5px;
    padding: 0 10px;
    color: #8F00FF;
}
.top:hover {
    -webkit-box-shadow: 0px 0px 64px 35px rgba(34, 60, 80, 0.2) inset;
    -moz-box-shadow: 0px 0px 64px 35px rgba(34, 60, 80, 0.2) inset;
    box-shadow: 0px 0px 64px 35px rgba(34, 60, 80, 0.2) inset;
}
.header__wrapper {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    height: 50px;
    align-items: center;
    padding: 0 10px;
}
</style>
