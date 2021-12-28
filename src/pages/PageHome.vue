<template>
    <div>
        <div>
            <h1>
                Eurosong
            </h1>
        </div>
        <!-- Page game -->
        <div>
             <button @click="changePage('game')">
                Show game
            </button>
        </div>
        <!-- Page ranking -->
        <div >
             <button @click="changePage('ranking')">
                Show ranking
            </button>
        </div>

    </div>
</template>

<script>
export default {
    name: "PageHome",
    methods: {
        changePage(page){
            this.$emit("change-page", page);
        }
    }
}
</script>

