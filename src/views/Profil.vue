<template>
  <Header />
  <div class="wrapper">
    {{ this.nom }}
    {{ this.prenom }}
    {{ this.email }}
  </div>
  <form @submit.prevent="modifier">
    <input type="date" name="" id="" @input="listen2" />
    <input type="text" name="" id="" />
    <input type="submit" value="Modifier profil" class="btn btn-primary" />
  </form>
</template>
<script>
import Header from "@/components/Header.vue";
const token = localStorage.getItem("token");

function getAge(b) {
  const a = b;
  console.log(a);

  var diff = Date.now() - a.getTime();
  var age = new Date(diff);
  return Math.abs(age.getUTCFullYear() - 1970);
}
export default {
  components: { Header },
  data() {
    return {
      nom: "",
      prenom: "",
      email: "",
      age2: "",
      occupation: "",
    };
  },

  methods: {
    listen2(event) {
      this.age2 = event.target.value;
      console.log(this.age2);
    },

    modifier() {
      const age1 = getAge(this.age2);
      console.log(age1);
    },
  },

  async mounted(evente) {
    const options = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token}`,
      },
    };

    const response = await fetch(
      "https://social-network-api.osc-fr1.scalingo.io/pandaru/user",
      options
    );

    const data = await response.json();
    console.log(data);
    this.nom = data.firstname;
    this.prenom = data.lastname;
    this.email = data.email;
    console.log(this.nom);
  },
};
</script>

<style scoped>
ul {
  display: flex;
  justify-content: space-around;
  list-style: none;
}
</style>
