<template>
  <div class="app" :class="{ 'has-background-black': darkMode }">
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
import { computed, inject } from "vue";
import ListingsList from './components/ListingsList';

import useDarkMode from './hooks/useDarkMode';

export default {
  name: 'App',
  setup() {
    // access the store
    const store = inject('store');
    const { darkMode, toggleDarkMode } = useDarkMode();

    // computed properties
    const darkModeButtonText = computed(() => {
      return darkMode.value ? "Light Mode" : "Dark Mode";
    });
    const listings = computed(() => store.state.listings); 
    const loading = computed(() => store.state.loading);

    // fire off actions for component created lifecycle stage
    store.actions.getListings();

    // return properties for component to access
    return {
      darkMode,
      darkModeButtonText,
      listings,
      loading,
      toggleDarkMode,
    };

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
