<template>
  <div class="wrapper">
    <form>
      <input type="text" placeholder="Commenter" @input="listen" />
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      comment1: "",
      array: [],
    };
  },

  methods: {
    comment(event) {
      event.preventDefault();

      console.log(event.target.id);
    },
  },
};
</script>

<style></style>
