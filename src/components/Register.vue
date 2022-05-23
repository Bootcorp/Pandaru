vue
<template>
  <div class="wrapper">
    <form @submit.prevent="">
      <input
        type="text"
        @input="user_nom"
        name="nom"
        id="nom"
        required
        placeholder="Nom"
        class="form-control"
      />
      <input
        type="text"
        name="prenom"
        id="prenom"
        required
        @input="user_prenom"
        placeholder="Prenom"
        class="form-control"
      />
      <input
        type="mail"
        required
        id="mail"
        @input="user_mail"
        placeholder="ema@il"
        class="form-control"
      />
      <input
        type="password"
        name="pass1"
        id="pass1"
        @input="user_mdp"
        placeholder="Mot de passe"
        class="form-control"
      />
      <input
        type="password"
        name="pass2"
        id="pass2"
        placeholder="Confirmez le mot de passe"
        class="form-control"
      />
      <input
        type="submit"
        value="valider"
        id="submit"
        @click="submit"
        class="btn btn-primary"
      />
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nom: "",
      prenom: "",
      mail: "",
      password: "",
      token: "",
      array: [],
    };
  },

  methods: {
    user_nom(event) {
      this.nom = event.target.value;

      console.log(this.info);
    },
    user_prenom(event) {
      this.prenom = event.target.value;
    },
    user_mail(event) {
      this.mail = event.target.value;
    },
    user_mdp(event) {
      this.password = event.target.value;
    },

    async submit() {
      const mail = this.mail;
      const nom = this.nom;
      const prenom = this.prenom;
      const password = this.password;

      const options = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          email: mail,
          password: password,
          firstname: nom,
          lastname: prenom,
        }),
      };

      const response = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/pandaru/register",
        options
      );
      const data = response.json();
      console.log(data);
      console.log(mail);
      console.log(nom);
      console.log(prenom);
      console.log(password);
      if (data.success) {
        console.log("bienvenue sur pandaru");
      }
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  align-items: center;
}
input {
  margin: 3vh;
  border-radius: 5px;
  height: 5vh;
}
.form-control {
  width: 25vw;
}
</style>
