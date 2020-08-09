<template>
  <div>
    <div class="container py-4">
      <h1>Posts</h1>

      <button
        type="button"
        class="btn btn-outline-primary"
        data-toggle="modal"
        data-target="#exampleModal"
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
        <tr v-for="item in items" :key="item._id">
          <td>{{ item.name }}</td>
          <td>{{ item.category }}</td>
          <td>
            <router-link
              :to="{ name: 'Edit', params: { id: item._id } }"
              class="btn btn-primary"
              >Edit</router-link
            >
          </td>
          <td>
            <button class="btn btn-danger" v-on:click="deleteItem(item._id)">
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
export default class Create extends Vue {
  @Prop() private msg!: string;
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
</style>
