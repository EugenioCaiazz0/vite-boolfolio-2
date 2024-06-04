<script>
import axios from 'axios'
import { store } from './data/store';

export default {
  
  data() {
    return {
      'projects': [],
      loading: true
    } 
  },

  methods:{
    getApi() {
      console.log('get API');
      axios.get(store.apiUrl)
      .then(result => {
        this.loading = false;
        this.projects = result.data //data // il secondo data ci mostra solo il numero di elementi definiti nel paginate
        console.log(result);
      })
      .catch(error => {
        this.loading = false;
        console.log(error);
      })
    }
  },
  mounted() {
      this.getApi()
    }
}
</script>

<template>
  <div class="main-wrapper">
    <div class="container"> 
      <h1> Vediamo di stampare questi projects </h1>
      <div v-if="!loading">
        <ul>
          <li v-for="project in projects"
          :key="project.id"> 
          {{ project.title }} - {{ project.author }}</li>
        </ul>
      </div>
      <p v-else> Loading... </p> <!-- da aggiungere error message -->
    </div>
  </div>
</template>

<style lang="scss" scoped>
</style>

<!-- aggiunta messaggio -->