<script setup lang="ts">
import ClickButton from './components/ClickButton/ClickButton.vue'
import { ref } from 'vue';
const theme = ref('dark')
function changeTheme() {
  theme.value = theme.value === 'dark' ? 'light' : 'dark'
}
</script>

<template>
  <v-app :theme="theme">
    <v-app-bar title="Double click tester">
      <v-spacer></v-spacer>
      <v-btn :prepend-icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'" text="Toggle theme"
        @click="changeTheme">
      </v-btn>
    </v-app-bar>
    <v-container class="d-flex flex-wrap" :oncontextmenu="(e: Event) => e.preventDefault()">
      <ClickButton click="Main"/>
      <ClickButton click="Auxiliary"/>
      <ClickButton click="Secondary"/>
    </v-container>
  </v-app>
</template>

<style scoped lang="scss">
</style>
