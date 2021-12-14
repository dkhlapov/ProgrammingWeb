<template>
    <div v-bind:class="'c-alert ' + customClasses" v-if="isActive" @click="hideAlert">
      {{message}}
    </div>
</template>

<script>
export default {
    name: "Alert",
    data(){
        return {
            isActive: true
        }
    },
    props: [
        "message",
        "customClasses"
    ],
    methods:{
        hideAlert(){
            this.isActive = false;
        }
    }
}
</script>