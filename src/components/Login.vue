<template>
  <div class="wrapper">
    <form action="" @submit.prevent="connexion">
      <input
        type="email"
        name=""
        placeholder="em@il"
        @input="user_mail"
        class="form-control"
      />
      <input type="password" name="" @input="user_password" />
      <input
        type="submit"
        value="se connecter"
       class="btn btn-primary"
      />
      <p>{{ this.message }}</p>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mail: "",
      password: "",
      token: "",
      array: [],
      message: "",
    };
  },

  methods: {
    user_mail(event) {
      this.mail = event.target.value;
    },
    user_password(event) {
      this.password = event.target.value;
    },

    async connexion() {
      const mail = this.mail;

      const password = this.password;

      const options = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          email: mail,
          password: password,
        }),
      };

      const response2 = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/pandaru/login",
        options
      );
      const data2 = await response2.json();
      console.log(data2);

      const token = data2.token;
      localStorage.setItem("token", token);

      console.log(this.token);
      if (data2.success) {
        console.log("bienvenue sur pandaru");
        Location: "/about";
        this.$router.push("accueil");
      } else if (!data2.success) {
        console.log(data2.message);
        this.message = data2.message;
      }
    },
  },
};
</script>

<style scoped>
.form-control {
  width: 25vw;
}
</style>
