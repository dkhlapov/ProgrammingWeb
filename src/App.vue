<template>
    <div id="app">
        <Navigation />
        <Button buttonText="Add warning alert" alertType="warning" alertMessage="Warning" 
        @add-message="addAlert"
        />

        <Alert :message=error.message :customClasses="error.customClasses" v-for="(error, index) in errors" :key="index"/>

        <h1>
            Eurosong festival
        </h1>

        <p>
            This is our voting application
        </p>
    </div>
</template>

<script>
    import Navigation from './components/Navigation.vue';
    import Alert from "./components/Alert.vue";
    import Button from "./components/Button.vue";


    export default {
        name: 'App',
        data(){
            return{
                errors: [
                    {
                        message: "Something went wrong"
                    },
                    {
                        message: "Warning",
                        customClasses: "warning"
                    },
                    {
                        message: "Success",
                        customClasses: "success"
                    }
        
                ]
            }
        },
        methods:{
            addAlert(message, type){
                this.errors.push({
                    message: message,
                    customClasses: type
                })
            }
        },
        components: {
            Navigation,
            Alert,
            Button
        }
    }
</script>

<style lang="scss">
    @import "./scss/style.scss";
</style>

