<template>
  <div>
    <div class="container py-4">
      <h1>Posts</h1>

      <button
        type="button"
        class="btn btn-outline-primary"
        data-toggle="modal"
        data-target="#exampleModal"
        @click="addPost"
      >
        Add Post
      </button>
    </div>

    <table class="table table-hover">
      <thead>
        <tr>
          <td>Post Name</td>
          <td>Post Category</td>
          <td>Edit</td>
          <td>Delete</td>
          <td></td>
        </tr>
      </thead>

      <tbody>
        <tr v-for="post in posts" :key="post._id">
          <td>{{ post.name }}</td>
          <td>{{ post.category }}</td>
          <td>
            <button class="btn btn-primary" v-on:click="editItem(post._id)">
              Edit
            </button>
          </td>
          <td>
            <button class="btn btn-danger" v-on:click="deleteItem(post._id)">
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <Create />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Index extends Vue {
  @Prop() private msg!: string;
  public posts: Array<object> = [
    {
      name: "Learn VueJS",
      category: "Vue"
    }
  ];
  // get postAdd(): string {
  //   return this.posts[0]+ ' '+ this.posts[1];
  // };

  public addPost(): void {
    alert("clicked");
    console.log(this.posts);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.container {
  text-align: center;
}

.table {
  margin: auto;
  padding: 50px;
}

td {
  padding: 35px;
}

.btn-primary {
  background: #1e88e5;
  color: white;
}

.btn-danger {
  background: #bb2124;
  color: white;
}
</style>
