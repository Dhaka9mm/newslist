<template>
  <div class="NewsList">
    <div class="container">
      <ul class="media-list">
        <li class="media" v-for="article in articles">
          <div class="media-left">
            <a v-bind:href="article.url" target="_blank">
              <img class="media-object" v-bind:src="article.urlToImage"/>
            </a>
          </div>
          <div class="media-body">
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">{{article.title}}</a>
            </h4>
            <h5>
              <i>by {{article.author}}</i>
            </h5>
            <p>{{article.description}}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ['source'],
  data () {
    return {
      articles: []
    }
  },
  methods: {
    updateSource(source) {
      this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=4ead3dd3065c4b51bcd483a455d0017c')
        .then((response) => {
          this.articles = response.data.articles;
        })
    }
  },
  watch: {
    source(value) {
      this.updateSource(value);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.media-object {
  width: 128px;
  padding: 10px;
}
.media {
  border-top: 1px solid lightgray;
  padding-top: 20px;
}

a {
  color: #42b983;
}
</style>
