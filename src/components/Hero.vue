<script setup>
import { onMounted } from "vue";
const props = defineProps({
  banner: {
    type: String,
    default: "",
    required: true,
  },
  title: {
    type: String,
    default: "",
    required: true,
  },
  description: {
    type: String,
    default: "",
    required: true,
  },
});

onMounted(() => {
  console.log("banner", props.banner);
});
</script>

<template>
  <v-container>
    <v-row align="center">
      <v-col cols="12" md="6">
        <div class="text-h2 font-weight-bold">{{ title }}</div>
        <div class="text-h6">{{ description }}</div>
      </v-col>
      <v-col cols="12" md="6">
        <v-img class="rounded" :src="banner" alt="banner image" cover></v-img>
      </v-col>
    </v-row>
  </v-container>
</template>
