<template>
  <v-app>
    <v-container grid-list-xs>
      <div>
        <div>
          <Navbar />
        </div>
        <h1>Simple weather app created by using Nuxtjs Framework for Vuejs</h1>
      </div>
    </v-container>
  </v-app>
</template>

<script>
import Navbar from '@/components/Navbar'
export default {
  components: {
    Navbar
  }
}
</script>