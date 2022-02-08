<template>
    <div class="main-banner">
        <div class="logo_nome">
            <router-link to="/">
            <br><br>
            <p><img src="/img/icreamicon.svg" alt="logo"></p>
            </router-link>
            <h1>Eugênio Sorveteria</h1>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Banner'
    }
</script>

<style scoped>

    .main-banner{
        background:#dd429c;
        background-size: cover;
        height: 400px;
    }

    .logo_nome{
        width: 250px;
        height: 250px;
        display: block;
        margin-left: auto;
        margin-right: auto;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    }
</style>