<template>
  <div id="listings">
    <Notification 
      :notification="notification"
      :toggleNotification="toggleNotification"
      :isDark="isDark" 
    />
    <div v-for="listing in listings" :key="listing.id">
      <ListingsListItem :listing="listing" :isDark="isDark" />
    </div>
    <button
      class="button is-light"
      :class="{ 'is-primary': darkMode, 'is-info': !darkMode }"
      @click="resetListings" 
      :disabled="listings.length === 3">
      Reset
    </button>
  </div>
</template>

<script>
import { onMounted, inject } from "vue";
import ListingsListItem from './ListingsListItem';
import Notification from './Notification';


import useDarkMode from '../hooks/useDarkMode';
import useNotification from "../hooks/useNotification";

export default {
  name: 'ListingsList',
  props: ['listings'],

  setup() {

    // access the store
    const store = inject('store');

    const { darkMode } = useDarkMode();

    const {
        notification,
        setNotification,
        toggleNotification,
    } = useNotification();

    // methods
    const resetListings = () => {
        setNotification("Listings have been reset!");
        return store.actions.resetListings();
    }

    // mounted lifecyle hook
    onMounted(() => {
        setNotification("Welcome to NewlineBnB!");
    });

    // return properties for component to access
    return { 
        darkMode,
        notification, 
        toggleNotification,
        resetListings
    }

  },

  components: {
    ListingsListItem,
    Notification
  },
}
</script>