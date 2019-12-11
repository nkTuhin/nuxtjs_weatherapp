<template>
  <div>
    <v-app-bar>
      <v-toolbar-title>
        <n-link class="white--text" to="/">Weather App</n-link>
      </v-toolbar-title>

      <v-spacer></v-spacer>
      <v-btn to="/about" rounded color="primary" dark>About</v-btn>
    </v-app-bar>
  </div>
</template>

<style>
a {
  text-decoration: none;
  color: white;
}
</style>