<template>
  <div class="main-container">
    <h1>Gerenciador de Pedidos</h1>
    <Painel />
  </div>
</template>

<script>
import Painel from '../components/Painel.vue'
export default {
  components: {
     Painel
      },
  name:'Pedidos'
}
</script>

<style scoped>

</style>
