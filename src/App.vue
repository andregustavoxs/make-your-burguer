<template>
  <div class="app-container">
    <Navbar :logo="logo_src" :alt="app_name"></Navbar>
    <div class="content">
      <router-view/>
    </div>
    <Footer />
  </div>
</template>

<style>
* {
  font-family: Helvetica;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.app-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.content {
  flex: 1;
}

.main-container {
  margin: 50px;
  min-height: 250px;
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}
</style>

<script>
import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue"

export default {
  components: {
    Navbar,
    Footer,
  },
  data() {
    return {
      logo_src: "img/logo.png",
      app_name: "Make your Burger",
    }
  }
}
</script>