<template>
  <div id="app">
    <h1>Leitor de RSS</h1>
    <input v-model="feedUrl" placeholder="Insira o URL do Feed RSS">
    <button @click="fetchFeed">Carregar Feed</button>
    
    <div v-if="loading">Carregando...</div>
    
    <ul v-if="feeds.length">
      <li v-for="(item, index) in feeds" :key="index">
        <h3>{{ item.title }}</h3>
        <p>{{ item.description }}</p>
        <a :href="item.link" target="_blank">Leia mais</a>
      </li>
    </ul>
    
    <div v-if="error" class="error">{{ error }}</div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      feedUrl: '',
      feeds: [],
      loading: false,
      error: null
    };
  },
  methods: {
    async fetchFeed() {
      if (!this.feedUrl) return;

      this.loading = true;
      this.error = null;
      
      try {
        const response = await axios.get(`https://api.rss2json.com/v1/api.json?rss_url=${this.feedUrl}`);
        this.feeds = response.data.items;
      } catch (err) {
        this.error = 'Erro ao carregar o feed';
      } finally {
        this.loading = false;
      }
    }
  }
};
</script>

<style scoped>
.error {
  color: red;
}
</style>
