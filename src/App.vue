<template>
  <Navbar :logo="logo_src" :alt="a"/> 
  <router-view/>
  <Footer />
</template>

<script>
import Footer from './components/Footer.vue';
import Navbar from './components/Navbar.vue';

  export default {
    name: 'App',
    components: {
      Navbar,
      Footer
    },
    data() {
      return {
        logo_src: '/img/logo.png',
        app_name: 'Make your burger'
      }
    }
  }
</script>

<style>
  * {
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: 71.2vh;
  }
  
  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
