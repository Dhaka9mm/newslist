<template>
  <div class="container" id="app">
    <SelectSource v-on:sourceChanged="sourceChanged"></SelectSource>
    <NewsList v-bind:source="source"></NewsList>
  </div>
</template>

<script>
  import SelectSource from './components/SelectSource.vue';
  import NewsList from './components/NewsList.vue';
export default {
  components: {
    SelectSource,
    NewsList
  },
  data() {
    return {
      source: ''
    }
  },
  methods: {
    sourceChanged(source) {
        this.source = source;
      }
  }
}
</script>

<style>
#app {

}
</style>
