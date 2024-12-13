<template>
  <nav id="nav">
    <router-link to="/" id="logo_url">
      <img :src="logo" :alt="alt" id="logo">
    </router-link>
    <router-link to="/">Home</router-link>
    <router-link to="/pedidos">Pedidos</router-link>
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
  border-bottom: 4px solid #FCBA03;
  padding: 1rem 5%;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

#nav #logo_url {
  margin: auto;
  margin-left: 0;
  padding: 0.5rem;
  transition: transform 0.3s ease;
}

#nav #logo_url:hover {
  transform: scale(1.05);
}

#logo {
  width: 45px;
  height: 45px;
}

#nav a {
  color: #FCBA03;
  text-decoration: none;
  margin: 0 1rem;
  padding: 0.5rem 1rem;
  font-weight: 600;
  font-size: 1.1rem;
  border-radius: 4px;
  transition: all 0.3s ease;
  position: relative;
}

#nav a:hover {
  color: #FFF;
  background-color: rgba(252, 186, 3, 0.1);
}

#nav a.router-link-active {
  color: #FFF;
  background-color: rgba(252, 186, 3, 0.2);
}

@media (max-width: 600px) {
  #nav {
    padding: 1rem 3%;
    flex-wrap: wrap;
    justify-content: center;
  }
  
  #nav #logo_url {
    margin: 0 0 1rem 0;
  }
  
  #nav a {
    margin: 0.5rem;
  }
}
</style>