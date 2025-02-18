<template>
  <nav id="nav">
    <router-link to="/" id="logourl">
      <img :src="logo" :alt="LT" id="logo">
    </router-link>
    <router-link to="/">Home</router-link> 
    <router-link to="/Pedidos">Pedidos</router-link>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  props: ["logo", "alt"]
}
</script>

<style scoped>
#nav {
  background-color: #222;
  border-bottom: 4px solid #111;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

#nav #logourl {
  margin: auto;
  margin-left: 0;
}

#logo {
  width: 40px;
  height: 40px;
}

#nav a {
  color: #fcba03;
  text-decoration: none;
  margin: 12px;
  transition: .5s;
}

#nav a:hover {
  color: #fff;
}

@media (max-width: 780px) {
  #nav {
    flex-direction: row;
    align-items: center;
  }
}
</style>