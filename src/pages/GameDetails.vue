<template>
  <div v-if="gameDetails" class="game-content">
    <div class="back">
       <button @click="back">Back</button>
    </div>
    <section class="image-container">
      <div>
        <img :src="gameDetails.background_image" :alt="gameDetails.name">
      </div>
    </section>
    <section class="details">
      <div class="flex-row space"></div>
      <div>
        <h3>{{gameDetails.name}}</h3>
      </div>
      <div>
        <p>{{gameDetails.description_raw}}</p>
      </div>
    </section>
  </div>
</template>

<script>
  import axios from 'axios'
  const API_KEY = process.env.VUE_APP_RAWG_KEY

  export default {
    name: 'GameDetails',
    data: () => ({
      gameDetails: null
    }),
    mounted() {
      this.getGameDetails()
    },
    methods: {
      async getGameDetails() {
        // Get game id from router here
        const gameId = this.$route.params.game_id
        const res = await axios.get(`https://api.rawg.io/api/games/${gameId}?key=${API_KEY}`)
        console.log(res)
        this.gameDetails = res.data
      }, 
      back() {
        this.$router.push(`/`)
      }
    }
  }
</script>
