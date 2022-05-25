<template>
  <ul>
    <li>
      <div class="img"></div>
    </li>
    <li>
      <router-link to="/accueil"
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          width="30"
          height="30"
          fill="rgb(117, 50, 1"
          class="bi bi-newspaper"
          viewBox="0 0 16 16"
        >
          <path
            d="M0 2.5A1.5 1.5 0 0 1 1.5 1h11A1.5 1.5 0 0 1 14 2.5v10.528c0 .3-.05.654-.238.972h.738a.5.5 0 0 0 .5-.5v-9a.5.5 0 0 1 1 0v9a1.5 1.5 0 0 1-1.5 1.5H1.497A1.497 1.497 0 0 1 0 13.5v-11zM12 14c.37 0 .654-.211.853-.441.092-.106.147-.279.147-.531V2.5a.5.5 0 0 0-.5-.5h-11a.5.5 0 0 0-.5.5v11c0 .278.223.5.497.5H12z"
          />
          <path
            d="M2 3h10v2H2V3zm0 3h4v3H2V6zm0 4h4v1H2v-1zm0 2h4v1H2v-1zm5-6h2v1H7V6zm3 0h2v1h-2V6zM7 8h2v1H7V8zm3 0h2v1h-2V8zm-3 2h2v1H7v-1zm3 0h2v1h-2v-1zm-3 2h2v1H7v-1zm3 0h2v1h-2v-1z"
          /></svg
      ></router-link>
    </li>
    <li>
      <router-link to="/profil"
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          width="30"
          height="30"
          fill="rgb(117, 50, 1"
          class="bi bi-house-door-fill"
          viewBox="0 0 16 16"
        >
          <path
            d="M6.5 14.5v-3.505c0-.245.25-.495.5-.495h2c.25 0 .5.25.5.5v3.5a.5.5 0 0 0 .5.5h4a.5.5 0 0 0 .5-.5v-7a.5.5 0 0 0-.146-.354L13 5.793V2.5a.5.5 0 0 0-.5-.5h-1a.5.5 0 0 0-.5.5v1.293L8.354 1.146a.5.5 0 0 0-.708 0l-6 6A.5.5 0 0 0 1.5 7.5v7a.5.5 0 0 0 .5.5h4a.5.5 0 0 0 .5-.5z"
          /></svg
      ></router-link>
    </li>

    <li>
      <button class="btn btn-primary" @click="disconnect1">Déconnexion</button>
    </li>

    <li><button @click="connect" class="btn btn-primary">Connexion</button></li>
  </ul>
  <router-view />
</template>

<style scoped>
.btn-primary {
  background: rgb(117, 50, 1);
  border: none;
  border-radius: 150px;
}
ul {
  display: flex;
  justify-content: space-around;
  list-style: none;

  background-color: rgb(236, 115, 27);
  height: 10vh;
  margin: 0;
  align-items: center;
}

.img {
  background: url(@/assets/panda.png) center/cover no-repeat;
  height: 16vh;
  width: 10vw;
}
</style>

}
<script>
export default {
  methods: {
    disconnect1() {
      localStorage.removeItem("token");
    },

    connect(e) {
      this.$router.push("/");
    },
  },
};
</script>
