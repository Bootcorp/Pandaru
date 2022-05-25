<template>
  <div class="bg"></div>
  <div class="wrapper">
    <Register />
    <div class="img"><h1>PANDARU</h1></div>
    <br />
    <Login />
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Amatic+SC:wght@700&family=Londrina+Solid:wght@900&family=Pacifico&display=swap");
template {
  background: rgb(204, 178, 162);
}
.wrapper {
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin-left: auto;
  margin-right: auto;
  flex-wrap: wrap;
  background: rgb(243, 164, 44);
  height: 100vh;
}

h1 {
  text-align: center;
  color: rgb(236, 115, 27);
  font-family: "Londrina Solid", cursive;
  font-size: 5em;
  letter-spacing: 2vh;
  -webkit-text-stroke: 2px black;
  text-shadow: 4px 4px 10px rgba(61, 61, 61, 0.782);
}

header {
  margin-left: auto;
  margin-right: auto;
  width: 100vw;
  display: flex;
  justify-content: space-around;
  align-items: center;
  align-content: center;
  text-align: center;

  background: rgb(204, 178, 162);
}
.img {
  background: url(@/assets/panda.png) center/cover no-repeat;
  height: 90vh;
  width: 40vw;
  z-index: 1;
}
.bg {
  position: absolute;
  background: url(@/assets/background.png) center/cover no-repeat;
  height: 98vh;
  width: 40vw;
  top: -10vh;
  left: 31vw;
  z-index: 0;
}
</style>

<script>
// @ is an alias to /src

import Register from "@/components/Register.vue";
import Login from "@/components/Login.vue";

export default {
  name: "HomeView",
  components: {
    Register,
    Login,
  },
};
</script>
