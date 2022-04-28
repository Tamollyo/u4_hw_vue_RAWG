<template>
  <div>
    <div class="search">
      <!-- Search Form Goes Here -->
      <form @submit="getSearchResults">
        <input type="text" :value="searchQuery" @input="handleChange">
        <button>Search</button>
      </form>
      <h2>Search Results</h2>
      <section  v-if="searched" class="search-results container-grid">
        <GameCard :key="result.id" :gameId="result.id" v-for="result in searchResults" :image="result.background_image" :name="result.name" @click="selectGame(result.id)"/>
      </section>
    </div>

    <div v-if="!searched" class="genres">
      <h2>Genres</h2>
      <section class="container-grid" >
        <GenreCard :key="genre.id" v-for="genre in genres" :image="genre.image_background" :name="genre.name"/>
      </section>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import GenreCard from '../components/GenreCard.vue'
  import GameCard from '../components/GameCard.vue'
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
      GenreCard, 
      GameCard
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
        const res = await axios.get(`https://api.rawg.io/api/games?key=${API_KEY}&search=${this.searchQuery}`)
        console.log(res)
        this.searchResults = res.data.results
        this.searched = true
      },
      handleChange(event) {
        this.searchQuery = event.target.value
        console.log(event)
      },
      selectGame(gameId) {
        this.$router.push(`/details/${gameId}`)
        console.log(gameId)
      }
    }
  }
</script>
