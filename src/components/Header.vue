<template>
  <ul>
    <li>Bienvenue sur Pandaru</li>
    <li><router-link to="/accueil">Actu</router-link></li>
    <li><router-link to="/profil">Mon profil</router-link></li>

    <li>
      <button class="btn btn-primary" @click="disconnect1">Déconnexion</button>
    </li>

    <li><button @click="connect" class="btn btn-primary">Connexion</button></li>
  </ul>
  <router-view />
</template>

<style scoped>
ul {
  display: flex;
  justify-content: space-around;
  list-style: none;
  border: solid yellow 2px;
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
