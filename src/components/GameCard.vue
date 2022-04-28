<template>
  <div class="card game-card">
    <div class="image-wrapper">
      <!-- Image Goes Here -->
      <img :src="image" :alt="name">
    </div>
    <div class="info-wrapper flex-col">
      <!-- Game Name Goes Here -->
      {{name}}
    </div>
  </div>
</template>

<script>
  export default {
    name: 'GameCard', 
    props: {
      name: String, 
      image: String, 
    }, 
  }
</script>
