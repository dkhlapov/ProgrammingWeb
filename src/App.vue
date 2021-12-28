<template>
    <div id="app">
        <!-- Page home -->
        <PageHome v-if="page == 'home'" @change-page="changePage" />
        <PageGame v-if="page == 'game'" @change-page="changePage" />
        <PageRanking v-if="page == 'ranking'" @change-page="changePage" />
        
    </div>
</template>

<script>
    import PageHome from "./pages/PageHome.vue"
    import PageGame from "./pages/PageGame.vue"
    import PageRanking from "./pages/PageRanking.vue"

    export default {
        name: 'App',
        data(){
            return{
                page: "home"
            }
        },
        methods:{
            changePage(page){
                this.page = page;

            }
        },
        components: {
           PageHome,
           PageGame,
           PageRanking
           
        }
    }
</script>

<style lang="scss">
    @import "./scss/style.scss";
</style>

