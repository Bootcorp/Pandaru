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
          <div class="post1">
            <strong> {{ item.lastname }}</strong>
            {{ item.content }}
          </div>

          <div class="post-comment">
            <Comment @input="listen"></Comment
            ><input
              type="submit"
              value="comment"
              :id="item._id"
              @click="dropcomment"
              class="btn btn-primary"
            />
          </div>

          <p class="commentaire">
            <strong>
              {{ item.comments.map((a) => a.lastname).join("") }}</strong
            >
            :
            <span>{{ item.comments.map((a) => a.content).join(" ") }}</span>
          </p>

          <p>
            {{
              item.likes.map((a) => a.firstname).join("") + " aime votre post"
            }}
          </p>

          <p>{{ this.message }}</p>
          <input
            type="submit"
            value="j'aime "
            @click="like"
            :id="'s' + item._id"
            class="btn btn-primary"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Amatic+SC:wght@700&family=Londrina+Solid:wght@100&family=Pacifico&display=swap");
.commentaire {
  font-size: 0.8em;
  margin-left: 5%;
  background: rgb(204, 178, 162);
  border-radius: 20px;
  width: 40vw;
  height: 5vh;
  margin-left: auto;
  margin-right: auto;
}
.post-comment {
  display: flex;
}
.post {
  font-size: 1.5em;
  margin-left: 5%;
  background: rgb(204, 178, 162);

  width: 100vw;
  height: 10vh;
  margin-left: auto;
  margin-right: auto;
}

.btn-primary {
  background: rgb(117, 50, 1);
  font-family: "Londrina Solid", cursive;
  letter-spacing: 0.2vw;
  border: none;
  height: 5vh;
  width: 8vw;
  margin: 1%;
}

li {
  list-style: none;
  background-color: rgb(236, 115, 27);
  text-align: center;
  color: white;
  font-family: "Londrina Solid", cursive;
  height: 30vw;
  border-radius: 10px;
}

.post1 {
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgb(117, 50, 1);
  width: 40%;
  border-radius: 10px;
  margin-left: auto;
  margin-right: auto;
  height: 15vh;
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
