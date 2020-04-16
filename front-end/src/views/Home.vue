<template>
<div class="home">
<img class="center" alt="Jacob" src="https://dw3jhbqsbya58.cloudfront.net/rosters/cfeda153-cbfc-46c2-95e1-8aff022efc11/7/f/5/7f53db19-1bb0-e611-8076-a0369f3c18ea/thumbnail.jpg?version=636845464623148690">
<h1>This is Jacob Fox</h1>
<p>The man</p>
<p>The myth</p>
<p>The legend</p>
<p>Go to the Admin page to upload your own pictures of the legendary Jacob Fox</p>
  <section class="image-gallery">
    <div class="image" v-for="item in items" :key="item.id">
      <h2>{{item.title}}</h2>
      <img :src="item.path" />
    </div>
  </section>

</div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
export default {
  name: 'Home',
  data() {
    return {
     items: [],
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
  },
}
</script>

<style scoped>
.image h2 {
  font-style: italic;
}

/* Masonry */
*,
*:before,
*:after {
  box-sizing: inherit;
}

.image-gallery {
  column-gap: 1.5em;
}

.image {
  margin: 0 0 1.5em;
  display: inline-block;
  width: 100%;
}

.image img {
  width: 100%;
  margin: auto;
}

/* Masonry on large screens */
@media only screen and (min-width: 1024px) {
  .image-gallery {
    column-count: 4;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .image-gallery {
    column-count: 3;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .image-gallery {
    column-count: 2;
  }
}

p {
  text-align: center;
}

h1 {
  text-align: center;
}

.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
a {
  text-align: center;
}
</style>
