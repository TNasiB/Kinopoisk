<template>
    <div class="search-wrapper flex">
        <input 
        @keyup.enter="sendQuery" 
        type="text" 
        class="search-input" 
        placeholder="Название фильма">

        <button 
        class="search-btn"
        @click="sendQuery"
        ></button>
    </div>
</template>

<script>
export default {
    name: 'SearchInput',
    methods: {
        sendQuery() {
            let query = document.querySelector(".search-input")
            let titleSite = document.querySelector(".films-title")

            this.$emit('send-query', query.value)

            titleSite.textContent = `Результат поиска по запросу ${query.value}`
            query.value = ""
        }
    }
}
</script>

<style scoped>
.search-wrapper {
    background-color: #fff;
    align-items: center;
    padding: 6px 6px;
    width: 420px;
    border-radius: 5px;
}
.search-input {
    border: none;
    flex: 1 1 auto;
    outline: none;
    padding-left: 10px;
}
.search-btn {
    background-image: url(../assets/img/search.svg);
    background-size: contain;
    background-repeat: no-repeat;
    background-color: transparent;
    width: 20px;
    height: 20px;
    border: none;
}
</style>
