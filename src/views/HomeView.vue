<template>
  <Banner/>
  <div class="main-container">
    <h1>Monte o seu lanche:</h1>
    <Forms/>
  </div>
</template>

<script>
import Banner from "../components/Banner.vue";
import Forms from "../components/Forms.vue";

export default {
  name: 'HomeView',
  components: {
    Banner,
    Forms,
  }
}
</script>

<style scoped>
</style>