<template>
    <div class="message-container">
            <h1>{{ mensagem }}</h1>
    </div>
</template>

<script>
export default {
    name:'Message',
    props:{
        mensagem: String
    }
}
</script>

<style scoped>
    .message-container{
        color: white;
        background: #dd429c;
        border: 2px solid black;
        border-radius: 3px;
        padding: 12px;
        max-width: 400px;
        margin: 30px auto;
        font-weight: normal;
        font-size: 8px;
    }
</style>