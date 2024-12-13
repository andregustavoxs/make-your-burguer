<template>
  <div id="main-banner">
    <div class="banner-overlay"></div>
    <div class="banner-content">
      <h1>Make Your Burger</h1>
      <p class="subtitle">Monte o hambúrguer do seu jeito</p>
      <div class="banner-cta">
        <router-link to="/" class="cta-button">
          <i class="fas fa-hamburger"></i>
          Fazer Pedido
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Banner"
  }
</script>

<style scoped>
#main-banner {
  background-image: url('/public/img/burger.jpg');
  background-position: center;
  background-size: cover;
  background-attachment: fixed;
  min-height: 85vh;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  overflow: hidden;
}

.banner-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    45deg,
    rgba(0, 0, 0, 0.7) 0%,
    rgba(0, 0, 0, 0.5) 100%
  );
  z-index: 1;
}

.banner-content {
  position: relative;
  z-index: 2;
  padding: 2rem 5%;
  max-width: 800px;
}

#main-banner h1 {
  color: #FFF;
  text-align: left;
  font-size: clamp(2rem, 4vw, 3.5rem);
  background-color: rgba(34, 34, 34, 0.9);
  padding: 20px 40px;
  margin-bottom: 1.5rem;
  border-radius: 10px;
  border-left: 6px solid #FCBA03;
  transform: translateX(-100%);
  animation: slideIn 1s forwards;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  white-space: nowrap;
  display: inline-block;
}

.subtitle {
  color: #FFF;
  font-size: clamp(1.5rem, 3vw, 2rem);
  margin-left: 60px;
  margin-bottom: 2rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  opacity: 0;
  animation: fadeIn 1s forwards 0.5s;
}

.banner-cta {
  margin-left: 60px;
  opacity: 0;
  animation: fadeIn 1s forwards 1s;
}

.cta-button {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background-color: #FCBA03;
  color: #222;
  padding: 1rem 2rem;
  border-radius: 50px;
  font-size: 1.2rem;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.cta-button:hover {
  background-color: #fff;
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(252, 186, 3, 0.3);
}

.cta-button i {
  font-size: 1.4rem;
}

@keyframes slideIn {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  #main-banner {
    min-height: 60vh;
    background-attachment: scroll;
  }

  .banner-content {
    padding: 1.5rem;
  }

  #main-banner h1 {
    padding: 20px 30px;
    margin-bottom: 1rem;
    border-left-width: 4px;
  }

  .subtitle {
    margin-left: 30px;
    margin-bottom: 1.5rem;
  }

  .banner-cta {
    margin-left: 30px;
  }

  .cta-button {
    padding: 0.8rem 1.5rem;
    font-size: 1.1rem;
  }
}
</style>