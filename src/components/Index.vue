<template>
  <div>
    <div class="container py-4">
      <h1>Posts</h1>

      <button
        type="button"
        class="btn btn-outline-primary"
        data-toggle="modal"
        data-target="#exampleModal"
        @click="addPostModal"
        
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
            <button class="btn btn-danger" v-on:click="deletePostButton(post._id)">
              Delete
            </button>
          </td>
        </tr>
      </tbody>

    <!-- Popup Modal -->

    <div id="myModal" class="modal" v-if="showModalPost">

        <!-- Modal content -->
        <div class="modal-content">
          <span class="close" @click="closeModal">&times;</span>

          <form v-on:submit.prevent="addPostButton">
          <div class="form-group">
            <label>Post Name: </label>
            <input
              type="text"
              id="post-name-id"
              class="form-control"
              v-model="tempName"
              required

            />
           
          </div>

          

            

            <div class="form-group">
              <br>
              <label for="categories">Select Category: </label>
              
                    <select
                      v-model="tempCategory"
                      v-on:change="getCategoryName($event)"
                      class="form-control form-control-sm"
                    >
                      <option value="CreateCategory">Create New Category</option
                      >
                      <option
                      
                        v-for="category in posts"
                        :key="category.id"
                        :value="category.category"
                        >{{ category.category }}</option
                      >
                    </select>
                  </div>

                  

          <div class="form-group">
            <br>
            <input type="submit" class="btn btn-primary" value="Add Post" />
          </div>
        </form>

        </div>

    </div>

    <div id="myModal2" class="modal" v-if="showModalCategory" >

        <!-- Modal content -->
        <div class="modal-content">
          <span class="close" @click="closeModalCategory">&times;</span>

          <form v-on:submit.prevent="addPostButton">
          <div class="form-group">
            <label>Category Name: </label>
            <input
              style="margin: 20px;"
              type="text"
              id="post-name-id"
              class="form-control"
              v-model="tempCategory"
              required

            />

            <br>
           
          </div>

          

            

            

          <div class="form-group">
            <input type="submit" class="btn btn-primary" value="Add Category" />
          </div>
        </form>

        </div>

    </div>

    </table>
    <Create />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Index extends Vue {
  @Prop() private msg!: string;
  private showModalPost = false;
  private showModalCategory = false;
  private emptyField = false;

  private tempName= '';
  private tempCategory = '';
  
  private posts: Array<object> = [
    {
      name: "Learn VueJS",
      category: "Vue"
    }
  ];
  // get postAdd(): string {
  //   return this.posts[0]+ ' '+ this.posts[1];
  // };

  public addPostModal(): void {
    this.showModalPost = true;
  }
  public closeModal(): void {
    this.showModalPost = false;
  }
  public closeModalCategory(): void {
    this.showModalCategory = false;
  }
  public addPostButton(nameValue: string, categoryValue: string): void {
      console.log('post added');
      this.posts.push({name: this.tempName, category: this.tempCategory});
  }
  public deletePostButton(postid: any): any {
      console.log('deleted');
      this.posts.splice(postid, 1);
  }

  public getCategoryName(e: any) {
      const value = e.target.value;
      if (value == "CreateCategory") {
        this.tempCategory = '';
        this.showModalCategory = true;
      };
    
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

.modal {
  
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 100px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

/* Modal Content */
.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
}

.form-control{
  
}

/* The Close Button */
.close {
  color: #aaaaaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}
</style>
