<script setup>
import PlaylistItems from "./PlaylistItems.vue";

defineProps({
  listPlaylist: {
    type: Array,
    default: () => [],
    required: true,
  },
});
</script>

<template>
  <v-container>
    <div class="d-flex flex-wrap justify-space-around">
      <div v-for="(item, index) in listPlaylist" :key="index">
        <PlaylistItems :item="item" />
      </div>
    </div>
  </v-container>
</template>
