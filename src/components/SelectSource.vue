<template>
  <div class="SelectSource">
    <div class="jumbotron">
      <h2><i class="fa fa-newspaper-o" aria-hidden="true"></i> News List</h2>
      <h4>Choose a news source</h4>
      <multiselect :options="sources"
                   track-by="id"
                   label="name"
                   :searchable="false"
                   :close-on-select="true"
                   :show-labels="false"
                   v-model="source"
                   @input="sourceChanged"
                   placeholder="Pick a source">
      </multiselect>
      <div v-if="source">
        <h6>{{source.description}}</h6>
        <a class="btn btn-success" v-bind:href="source.url" target="_blank">Go to {{source.name}} website</a>
      </div>
    </div>
  </div>
</template>

<script>
  import Multiselect from 'vue-multiselect';

  export default {
    components: {
      Multiselect
    },
    data () {
      return {
        sources: [],
        source: ''
      }
    },
    created:function () {
      this.$http.get('https://newsapi.org/v1/sources?language=en')
        .then((response) => {
          this.sources = response.data.sources;
      });
    },
    methods: {
      sourceChanged(e) {
        this.$emit('sourceChanged', e.id);
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
<style scoped>

</style>
