<template>
  <b-container>
    <input class="form-control" placeholder="Search" type="text" v-model="filter"/>
    <div class="full-logos-items text-center">
      <div class="item" v-for="post in filteredPosts" :key="post.title">
        <router-link class="nav-link" :to="`/frontend-helper/item?page=${post.link[0]}`" exact>
          <div v-if="post.img != 'notfound'">
            <b-img-lazy :src="require(`../assets/images/items/${post.img}`)"/>
          </div>
          <div v-else>
            <b-img-lazy :src="`https://lightwidget.com/widgets/empty-photo.jpg`" width="100"/>
          </div>
        </router-link>
      </div>
      <div class="not-found" v-if="filteredPosts.length < 1">
        <h4>Not Found :( <br>If you need it you can add it on <a href="https://github.com/moumen-soliman/frontend-helper" target="_blank">Github Repo</a></h4>
      </div>
    </div>
  </b-container>
</template>

<script>
import item from "../storedData/items.json";

export default {
  name: "Home", // this is the name of the component
  data() {
    return {
      filter: "",
      posts: item
    };
  },
  computed: {
    filteredPosts () {
      const { filter, posts } = this;
      return posts
        .filter(post => post.title.toLowerCase().includes(filter.toLowerCase()))
    }
  }
};
</script>

<style lang="scss" scoped>
.not-found {
  h4 {
    margin: 28vh auto;
    a {
      text-decoration: underline;
    }
  }
}
.full-logos-items {
  padding: 30px 0;
  .item {
    margin: auto;
    display: inline-block;
    img {
      width: 100px;
      -webkit-filter: grayscale(97%);
      &:hover {
        -webkit-filter: grayscale(0);
      }
    }
  }
}
</style>
