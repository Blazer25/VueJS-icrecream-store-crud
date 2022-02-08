<template>
<div>
  <NavBar :logo="src_logo" :alt="name_app"/>
  <router-view/>
  <Footer />
</div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Footer from './components/Footer.vue'

export default {
  components:{
    NavBar,
    Footer
  },
  data(){
    return{
      src_logo:"/img/icreamicon.svg",
      name_app: "/img/icecreamwp.jpg"
    }
  }
  
}
</script>

<style>
  *{ 
    margin: 0;
    padding: 0;
    border: none;
    text-decoration: none;
    box-sizing: border-box;
  }

  html{
    background: white;
  }

  .screen-only {
    position: absolute;
    height: 1px;
    width: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip-path: rect(0, 0, 0, 0);
    white-space: nowrap;
    border-width: 0;
}

  .main-container{
    /* margin: 50px; */
    min-height: 250px;
  }
  
  h1{
    text-align: center;
  }
</style>
