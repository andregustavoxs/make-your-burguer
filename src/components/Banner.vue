<template>
  <div id="main-banner">
    <h1>Make Your Burger</h1>
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
    min-height: 80vh;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    padding: 20px;
  }

  #main-banner h1 {
    color: #FFF;
    text-align: left;
    font-size: clamp(3rem, 7vw, 80px);
    background-color: #222;
    padding: 30px 60px;
    margin-left: 40px;
    border-radius: 10px;
  }

  @media (max-width: 768px) {
    #main-banner {
      min-height: 50vh;
      padding: 10px;
    }

    #main-banner h1 {
      padding: 20px 40px;
      margin-left: 20px;
      width: auto;
      max-width: 90%;
      border-width: 3px;
    }
  }

</style>