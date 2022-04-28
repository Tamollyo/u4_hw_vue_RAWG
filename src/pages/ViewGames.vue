<template>
  <div className="container-grid">
    <GameCard :key="game.id" :gameId="game.id" v-for="game in games" :image="game.background_image" :rating="game.rating" :name="game.name" @click="selectGame(game.id)"/>
  </div>
</template>

<script>
  import axios from 'axios'
  const API_KEY = process.env.VUE_APP_RAWG_KEY
  import GameCard from "../components/GameCard.vue"

  export default {
    name: 'ViewGames',
    data: () => ({
      games: []
    }),
    components: {
      GameCard
    }, 
    mounted() {
      this.getGamesByGenre()
    },
    methods: {
      async getGamesByGenre() {
        // Get Genre Id here
        const genreId = this.$route.params.genre_id
        const res = await axios.get(`https://api.rawg.io/api/games?genres=${genreId}&key=${API_KEY}`)
        this.games = res.data.results
      },      
      selectGame(gameId) {
        this.$router.push(`/details/${gameId}`)
        console.log(gameId)
      },
    }
  }
</script>
