<script setup>
defineProps({
  item: {
    type: Object,
    default: () => {},
    required: true,
  },
});
</script>

<template>
  <v-card class="mx-auto my-12" max-width="350">
    <v-img
      height="250"
      :src="item.url"
      cover
      v-if="item.type === 'image'"
    ></v-img>
    <!-- :src="item.url" saya belum dapat menampilkan video yang ada pada API -->
    <iframe
      v-else-if="item.type === 'video'"
      height="250"
      width="100%"
      src="https://www.youtube.com/embed/ePmYL1L3psg"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen
    ></iframe>

    <v-card-item>
      <v-card-title>{{ item.title }}</v-card-title>

      <div>
        <span>{{ item.description }}</span>
      </div>
    </v-card-item>
  </v-card>
</template>
