<template>
  <div class="header">
    <div class="title-wrapper container d-flex justify-content-between align-items-center mb-3">
      <h1 class="title">Chuck Norris Facts</h1>
      <button class="btn btn-primary" @click="fetchRandomJoke" data-bs-toggle="modal" data-bs-target="#randomJokeModal">
        Random Joke
      </button>
    </div>
    <CategorySelector :categories="categories" :selected="selectedCategory" @update:selected="handleCategoryChange" />
  </div>
  <div class="container main">
    <JokesTable :jokes="jokes" />
  </div>
  <RandomJokeModal :joke="randomJoke" />
</template>

<script>
import axios from 'axios';
import CategorySelector from './components/CategorySelector.vue';
import JokesTable from './components/JokesTable.vue';
import RandomJokeModal from './components/RandomJokeModal.vue';

export default {
  components: { CategorySelector, JokesTable, RandomJokeModal },
  data() {
    return {
      categories: [],
      selectedCategory: '',
      jokes: [],
      randomJoke: '',
    };
  },
  async created() {
    const { data } = await axios.get('https://api.chucknorris.io/jokes/categories');
    this.categories = data;
    this.selectedCategory = data[0];
    this.fetchJokes(data[0]);
  },
  mounted() {
    document.title = 'Chuck Norris Facts';
  },
  methods: {
    handleCategoryChange(category) {
      this.selectedCategory = category;
      this.fetchJokes(category);
    },
    async fetchJokes(category) {
      this.jokes = [];
      const jokeRequests = Array.from({ length: 4 }, () =>
        axios.get('https://api.chucknorris.io/jokes/random', { params: { category } })
      );
      const responses = await Promise.all(jokeRequests);
      this.jokes = responses.map(response => response.data);
    },
    async fetchRandomJoke() {
      const { data } = await axios.get('https://api.chucknorris.io/jokes/random');
      this.randomJoke = data.value;
    },
  },
};
</script>

<style>
body {
  overflow-x: hidden;
  background-color: #000000f8 !important;
  background-image: url(./assets/img/chuck.png);
  background-blend-mode: multiply;
  /* position: relative; */
}

.header {
  width: 100%;
  background-color: black;
  padding:15px 5px;
}

.title {
  color: white;
}

.btn-primary,
.nav-link.active {
  background-color: purple !important;
  border-color: purple!important;;

}
@media (max-width: 600px) {
  .title-wrapper {
    flex-direction: column;
  }
}
</style>