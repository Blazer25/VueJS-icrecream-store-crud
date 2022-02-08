<template>
  <div id="nav">
      <router-link to="/">
          <img :src="logo" :alt="alt" id="logo" class="urlLogo">
      </router-link>
    <router-link to="/">Home</router-link>
    <router-link to="/Pedidos">Pedidos</router-link>
  </div>
    
</template>

<script>
export default {
    name: 'NavBar',
    props: ["logo","alt"]
}
</script>

<style scoped>
  #nav{
    padding: 10px 30px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    background: #ffc0cb;
  }

  #nav .urlLogo{
    width: 47px;
    height: 47px;
  }
  
  #nav a{
    text-decoration: none;
    font-size: 23px;
    color: black;
    margin: 15px;
    transition: 0.5s;
  }

  #nav a:hover{
    color: white;
    margin: 10px;
  } 

</style>