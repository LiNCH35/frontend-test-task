<template>
    <div id="app">
        <project/>
    </div>
</template>

<script>
    import Project from "./components/project/Project";
    import {provideSessionStorage} from  './plugins/sessionStorage';

    export default {
        name: 'App',
        components: {
            Project
        },

        setup() {
            provideSessionStorage();
        },
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
