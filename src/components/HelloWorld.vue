<template>
  <v-container class="fill-height">
    <v-responsive class="align-centerfill-height mx-auto" max-width="900">
      <div class="text-center">
        <div class="text-body-2 font-weight-light mb-n1">Welcome to</div>

        <h1 class="text-h2 font-weight-bold">The Library</h1>
        <br>
        <v-btn @click="getRandomCard" prepend-icon="mdi-feature-search" size="large" variant="outlined">
          Get a Random Card
        </v-btn>
        <br><br>
        <h1> {{ cardName }} </h1>
        <br>
        <v-img height="450" :src="photoLink" />
      </div>

      <div class="py-4" />
    </v-responsive>
  </v-container>
</template>

<script setup>
//  
import axios from 'axios';
import { ref } from 'vue'

const cardName = ref("")
const photoLink = ref("")

const count = ref(0)

function increment() {
  count.value++
}

async function getRandomCard() {
  const response = await axios.get('https://api.scryfall.com/cards/random')
    .then((response) => {
      cardName.value = response.data.name
      photoLink.value = response.data.image_uris.png
    })

}
</script>
