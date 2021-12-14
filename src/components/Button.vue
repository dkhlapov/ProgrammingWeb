<template>
    <button @click="clicked">
        {{buttonText}}
    </button>
</template>

<script>
    export default {
        name: "Button",
        props: [
            "alertMessage",
            "alertType",
            "buttonText"
        ],
        methods: {
            clicked(){
                console.log("You clicked a button");
                this.$emit("add-message", this.alertMessage, this.alertType)
            }
        }
    }
</script>