<template>
  <div>
    <div class="search">
      <!-- Search Form Goes Here -->
      <h2>Search Results</h2>
      <section class="search-results container-grid"></section>
    </div>

    <div class="genres">
      <h2>Genres</h2>
      <section class="container-grid">
        <GenreCard :key="genre.id" v-for="genre in genres" :image="genre.image_background" :name="genre.name"  />
      </section>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import GenreCard from '../components/GenreCard.vue'
  const API_KEY = process.env.VUE_APP_RAWG_KEY

  export default {
    name: 'HomePage',
    data: () => ({
      genres: [],
      searchQuery: '',
      searchResults: [],
      searched: false
    }),
    components: {
      GenreCard
    },
    mounted() {
      this.getGenres()
    },
    methods: {
      async getGenres() {
        const res = await axios.get(`https://api.rawg.io/api/genres?key=${API_KEY}`)
        console.log(res)
        this.genres = res.data.results
      },
      async getSearchResults(e) {
        e.preventDefault()
      },
      handleChange(event) {
        console.log(event)
      },
      selectGame(gameId) {
        console.log(gameId)
      }
    }
  }
</script>
