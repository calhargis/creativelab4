<template>
<div class="admin">
<h1>Submit your own photos and comments about Jacob!</h1>
  <div class="heading">
    <h2>Add Your Photo of Jacob here</h2>
  </div>
  <div class="add">
    <div class="form">
      <input v-model="title" placeholder="Title">
      <p></p>
      <input type="file" name="photo" @change="fileChanged">
      <button @click="upload">Upload</button>
    </div>
    <br><br><br>
    <div class="upload" v-if="addItem">
      <h2>{{addItem.title}}</h2>
      <img :src="addItem.path" />
    </div>
  </div>
  <div class="heading">
      <h2>Delete Photos</h2>
    </div>
    <div class="edit">
      <div class="form">
        <input v-model="findTitle" placeholder="Search">
        <div class="suggestions" v-if="suggestions.length > 0">
          <div class="suggestion" v-for="s in suggestions" :key="s.id" @click="selectItem(s)">{{s.title}}
          </div>
        </div>
      </div>
      <div class="upload" v-if="findItem">
        <input v-model="findItem.title">
        <p></p>
        <img :src="findItem.path" />
      </div>
      <div class="actions" v-if="findItem">
        <button @click="deleteItem(findItem)">Delete</button>
      </div>
    </div>
    <button @click="editItem(findItem)">Edit</button>
</div>
</template>



<script>
import axios from 'axios';
export default {
  name: 'Admin',
  data() {
    return {
      title: "",
      file: null,
      addItem: null,
      items: [],
      findTitle: "",
    findItem: null,
    }
  },
  computed: {
    suggestions() {
      let items = this.items.filter(item => item.title.toLowerCase().startsWith(this.findTitle.toLowerCase()));
      return items.sort((a, b) => a.title > b.title);
    }
  },
  created() {
    this.getItems();
  },

  methods: {
    async getItems() {
      try {
        let response = await axios.get("/api/items");
        this.items = response.data;
        return true;
      } catch (error) {
        console.log(error);
      }
    },
    fileChanged(event) {
      this.file = event.target.files[0]
    },
    async upload() {
      try {
        const formData = new FormData();
        formData.append('photo', this.file, this.file.name)
        let r1 = await axios.post('/api/photos', formData);
        let r2 = await axios.post('/api/items', {
          title: this.title,
          path: r1.data.path
        });
        this.addItem = r2.data;
      } catch (error) {
        console.log(error);
      }
    },
    selectItem(item) {
      this.findTitle = "";
      this.findItem = item;
      console.log(this.findItem);
    },
    async deleteItem(item) {
      try {
        console.log("in delete route");
        console.log(item._id);
        await axios.delete("/api/items/" + item._id);
        this.findItem = null;
        this.getItems();
        return true;
      } catch (error) {
        console.log(error);
      }
    },
    async editItem(item) {
      try {
        await axios.put("/api/items/" + item._id, {
          title: this.findItem.title,
        });
        this.findItem = null;
        this.getItems();
        return true;
      } catch (error) {
        console.log(error);
      }
    },
  }
}
</script>



<style scoped>
.image h2 {
  text-align: center;
  font-size: 1em;
}

.heading {
  margin: auto;
  text-align: center;
}


.add,
.edit {
  margin: auto;
  text-align: center;
}


/* Form */
input,
textarea,
select,
button {
  font-family: Arial;
  font-size: 1em;
  text-align: center;
  margin: auto;
}

.form {
  text-align: center;
  margin: auto;
}

/* Uploaded images */
.upload h2 {
  margin: 0px;
}

.upload img {
  max-width: 300px;
  text-align: center;
  margin: auto;
}

/* Suggestions */
.suggestions {
  width: 200px;
  border: 1px solid #ccc;
  text-align: center;
  margin: auto;
}

.suggestion {
  min-height: 20px;
  text-align: center;
  margin: auto;
}

.suggestion:hover {
  background-color: #5BDEFF;
  color: #fff;
  text-align: center;
  margin: auto;
}

h1 {
  text-align: center;
}

button {
text-align: center;
margin: auto;
}
</style>
