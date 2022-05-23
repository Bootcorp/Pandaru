<template>
  <div class="wrapper">
    <form @submit="partager">
      <input type="text" name="" id="" placeholder="titre" @input="listen" />
      <input
        type="text"
        name=""
        id=""
        placeholder="commentaire"
        @input="listen2"
      />
      <input type="submit" value="Partager" class="btn btn-primary" />
    </form>
  </div>
</template>

<script>
const token = localStorage.getItem("token");
export default {
  data() {
    return {
      title: "",
      content: "",
    };
  },
  methods: {
    listen(event) {
      this.title = event.target.value;
    },
    listen2(event) {
      this.content = event.target.value;
    },

    async partager() {
      const title = this.title;
      const content = this.content;

      const options = {
        method: "POST",
        headers: {
          "Content-Type": "application/json ",
          Authorization: `Bearer ${token}`,
        },
        body: JSON.stringify({
          title: this.title,
          content: this.content,
        }),
      };

      const response = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/pandaru/post",
        options
      );

      const data = await response.json();
      console.log(data);
      console.log("ok");
      console.log(this.title);
      console.log(this.content);
    },
  },
};
</script>

<style></style>
