<template>
    <nav class="nav">
        <router-link to="/" class="router">Home Page</router-link>
        <router-link to="/employees" class="router">Employees Page</router-link>
    </nav>
    <br/>
    <router-view/>
</template>

<script>
    export default {
        name: 'App'
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

    .nav{
        float: left;
        font-weight: bold;
        font-size: large;
    }

    .router{
        text-decoration: none;
        padding-left: 10px;
    }

</style>
