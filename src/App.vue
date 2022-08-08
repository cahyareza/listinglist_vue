<template>
  <div class="app" :class="{ 'has-background-black': isDark }">
    <div class="container is-max-desktop py-6 px-4">
      <div v-if="loading">
        <progress class="progress is-small is-info" max="100">60%</progress>
      </div>
      <div v-if="!loading">
        <ListingsList :listings="listings" :isDark="isDark" />
      </div>
      <button class="button is-small is-pulled-right my-4"
        @click="toggleDarkMode">
        {{ darkModeButtonText }}
      </button>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import { mapGetters } from 'vuex';
import ListingsList from './components/ListingsList';

export default {
  name: 'App',
  setup() {
    // reactive data properties
    const isDark = ref(false);

    // computed properties
    const darkModeButtonText = computed(() => {
      return isDark.value ? "Light Mode" : "Dark Mode";
    });
  },
  components: {
    ListingsList
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
