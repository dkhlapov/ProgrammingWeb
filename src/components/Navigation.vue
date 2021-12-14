<template>
    <nav class="c-nav">
        <h2 v-html="title" v-on:click="toggleNav"></h2>
        <ul class="c-nav-list" v-if="showNavigation">
            <li class="c-nav-list-item" v-for="(item, index) in items" v-bind:key="index">
                <a v-bind:href="item.url">
                    {{item.text}}
                </a>
            </li>
        </ul>
    </nav>
</template>
    
<script>

export default {
    name: "Navigation",
    data(){
        return{
            showNavigation: false,
            title: "Home <strong>page</strong>",
            items: [
                {
                    text: "Home"
                },
                {
                    text: "Voting"
                }
            ]
        }
    },
    methods: {
        toggleNav(){
            this.showNavigation = !this.showNavigation;
        }
    }
}
</script>
