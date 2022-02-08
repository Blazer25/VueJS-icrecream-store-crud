<template>
 
  <div class="main-container">
     <Banner/>
    <FormSorvete />
  </div>
</template>

<script>
import Banner from '../components/Banner.vue'
import FormSorvete from '../components/FormSorvete.vue'

export default {
  name: 'Home',
  components: {
    Banner,
    FormSorvete
    }

  }

</script>
