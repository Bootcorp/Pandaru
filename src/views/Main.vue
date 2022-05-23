<template>
  <Header />
  <PostView class="post" />
  <div class="wrapper">
    <div class="list_container">
      <ul class="list-group">
        <li
          v-for="(item, index) in this.array"
          :key="index"
          class="list-group-item"
        >
          {{ item.lastname }}
          {{ item.content }}
          <p>
            {{ item.comments.map((a) => a.firstname).join("") }} :
            <span>{{ item.comments.map((a) => a.content).join(" ") }}</span>
          </p>

          <Comment @input="listen"></Comment
          ><input
            type="submit"
            value="partager comment"
            :id="item._id"
            @click="dropcomment"
            class="btn btn-primary"
          />

          <input
            type="submit"
            value="j'aime"
            @click="like"
            :id="'s' + item._id"
            class="btn btn-primary"
          />
          <p>
            {{
              item.likes.map((a) => a.firstname).join("") + " aime votre post"
            }}
          </p>

          <p>{{ this.message }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
li {
  list-style: none;
}

.post {
  border: solid blueviolet 2px;
}

Header {
  border: solid yellow 2px;
}
</style>

<script>
import Header from "@/components/Header.vue";
import PostView from "@/components/PostView.vue";
import Comment from "@/components/Comment.vue";
const token = localStorage.getItem("token");

export default {
  components: {
    Header,
    PostView,
    Comment,
  },

  data() {
    return {
      array: [],
      id: "",
      content1: "",
      message: "",
    };
  },

  methods: {
    async like(event) {
      const id2 = event.target.id;
      const id_replace = id2.replace("s", "");
      console.log(id_replace);
      this.id = id_replace;
      const id_def = this.id;

      const options3 = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${token}`,
        },
        body: JSON.stringify({ postId: id_def }),
      };

      const response3 = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/pandaru/post/like",
        options3
      );
      const data3 = await response3.json();

      if (!data3.user) {
        this.message = data3.message;
      }
      console.log(data3);
      console.log(this.id);
    },

    listen(event) {
      console.log(event.target.value);
      this.content1 = event.target.value;
    },

    async dropcomment(event) {
      /*       window.location.reload(); */
      const id = event.target.id;

      const content2 = this.content1;
      const option = {
        method: "POST",
        headers: {
          "Content-Type": "application/json ",
          Authorization: `Bearer ${token}`,
        },
        body: JSON.stringify({
          postId: id,
          content: content2,
        }),
      };

      const response = await fetch(
        "https://social-network-api.osc-fr1.scalingo.io/pandaru/post/comment",
        option
      );
      const data1 = await response.json();
      console.log(data1);
    },
  },

  async mounted() {
    const options = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
      },
    };

    const response = await fetch(
      "https://social-network-api.osc-fr1.scalingo.io/pandaru/posts",
      options
    );
    const data = await response.json();
    console.log(data);
    this.id = data.posts.userid;
    this.array = data.posts;
    console.log(data.posts);
  },
};
</script>
