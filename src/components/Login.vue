<template>
  <form action="" @submit.prevent="connexion">
    <h2>Se connecter</h2>
    <input
      type="email"
      name=""
      placeholder="em@il"
      @input="user_mail"
      class="form-control"
    />
    <input
      type="password"
      name=""
      @input="user_password"
      class="form-control"
    />
    <input type="submit" value="se connecter" class="btn btn-primary" />
    <p>{{ this.message }}</p>
  </form>
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
@import url("https://fonts.googleapis.com/css2?family=Amatic+SC:wght@700&family=Londrina+Solid:wght@900&family=Pacifico&display=swap");
form {
  background-color: rgba(236, 114, 27, 0.696);
  border-radius: 15px;
  box-shadow: 4px 4px 10px rgba(61, 61, 61, 0.782);
  transform: translateX(-33vh);
}

.form-control {
  display: flex;
  width: 15vw;
}

h2 {
  font-size: 2em;
  text-align: center;
  padding: 0.5vh;
  font-family: "Londrina Solid", cursive;
  color: white;
  letter-spacing: 1vh;
}
.btn-primary {
  background: rgb(117, 49, 1);
  border: none;
}
input {
  margin: 3vh;
  border-radius: 5px;
  height: 5vh;
  width: 15vw;
}
</style>
