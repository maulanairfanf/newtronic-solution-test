<script setup>
defineProps({
  logo: {
    type: String,
    default: "",
    required: true,
  },
});
</script>

<template>
  <v-container>
    <v-app-bar app>
      <v-toolbar-title>
        <v-img :src="logo" width="250"></v-img>
      </v-toolbar-title>
    </v-app-bar>
  </v-container>
</template>
