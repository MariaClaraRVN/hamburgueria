<template>
  <Navbar :logo="logo_src" :alt="app_name" />
  <router-view />
  <Footer/>
</template>

<script>
import Navbar from './components/NavBar.vue';
import Footer from './components/Footer.vue';

export default {
  components: {
    Navbar,
    Footer
  },

  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Faça seu hambúrguer"
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat", serif;
}

.main-container{
  margin: 50px;
  min-height: 100vh;
}

h1{
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
  font-family: "Luckiest Guy", serif;
}

@media (max-width: 768px) {
  .main-container {
    margin: 20px;
  }
  h1 {
    font-size: 28px;
  }
}
</style>
