<template>
  <div class="card">
    <img
      class="card-img-top"
      :src="item.urlToImage"
      :alt="item.title"
      v-if="item.urlToImage"
    />
    <div class="card-body">
      <h4 class="card-title">{{ item.title }}</h4>
      <p class="card-text">{{ item.description }}</p>
      <small class="card-text text-secondary font-italic text-small">{{
        dateFormat
      }}</small>
      <hr />
      <a :href="item.url" class="btn btn-info">Ver noticia completa ...</a>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "NewsPanel",
  props: ["item"],
  computed: {
    dateFormat() {
      moment.locale("es");
      return moment(this.item.publishedAt).format("MMMM D YYYY, h:mm:ss a");
    }
  }
};
</script>
