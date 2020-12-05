<template>
  <div id="app">
    <nav class="navbar navbar-expand-md navbar-light bg-light mb-3">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler d-lg-none"
        type="button"
        data-toggle="collapse"
        data-target="#collapsibleNavId"
        aria-controls="collapsibleNavId"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="collapsibleNavId">
        <ul class="navbar-nav mr-auto mt-2 mt-lg-0">
          <li class="nav-item active">
            <a class="nav-link" href="#">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Link</a>
          </li>
        </ul>
      </div>
    </nav>
    <div class="container">
      <h2 class="text-center mb-4">Noticias de Colombia</h2>
      <div class="col-md-8 mx-auto mb-3">
        <div class="d-flex justify-content-between align-items-baseline">
          <label for="category" class="mb-2 mr-sm-2">Categoría: </label>
          <select
            id="category"
            class="custom-select mb-2"
            v-model="category"
            @change="loadNews"
          >
            <option
              v-for="category in categories"
              :key="category.value"
              :value="category.value"
              >{{ category.name }}</option
            >
          </select>
        </div>
      </div>
      <div class="row mx-auto mb-3" v-if="news.length">
        <div class="col-md-3"><news-panel :item="news[0]" /></div>
        <div class="col-md-3"><news-panel :item="news[1]" /></div>
        <div class="col-md-3"><news-panel :item="news[2]" /></div>
        <div class="col-md-3"><news-panel :item="news[3]" /></div>
      </div>
      <div>
        <!-- <pre>
          {{ $data }}
        </pre> -->
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap";
import NewsPanel from "./components/NewsPanel";
const axios = require("axios");
axios.defaults.baseURL = "https://newsapi.org";
axios.defaults.headers = {
  "X-Api-Key": process.env.VUE_APP_API_NEWS_KEY
};

export default {
  name: "App",
  components: {
    NewsPanel
  },
  data() {
    return {
      categories: [
        { value: "science", name: "Ciencia" },
        { value: "sports", name: "Deportes" },
        { value: "entertainment", name: "Entretenimiento" },
        { value: "general", name: "General" },
        { value: "business", name: "Negocios" },
        { value: "health", name: "Salud" },
        { value: "technology", name: "Tecnología" }
      ],
      category: "technology",
      news: []
    };
  },
  mounted() {
    this.loadNews();
  },
  methods: {
    async loadNews() {
      // const apiKey = process.env.VUE_APP_API_NEWS_KEY;
      // let url = `https://newsapi.org/v2/top-headlines?country=co&category=${this.category}&apiKey=${apiKey}`;
      let url = `/v2/top-headlines?country=co&category=${this.category}`;
      // axios
      //   .get(url)
      //   .then(response => {
      //     this.news = response.data.articles;
      //   })
      //   .catch(error => {
      //     console.log(error);
      //   });
      try {
        const response = await axios.get(url);
        this.news = response.data.articles;
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>

<style>
@import "~bootstrap/dist/css/bootstrap.css";
</style>
