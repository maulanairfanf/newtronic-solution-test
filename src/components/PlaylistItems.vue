<script setup>
import axios from "axios";
import { ref } from "vue";

const props = defineProps({
  item: {
    type: Object,
    default: () => {},
    required: true,
  },
});

async function handleDownload() {
  // belum dapat mendownload video
  const imageUrl = props.item.url;
  const type =
    props.item.type === "image"
      ? `${props.item.title}.jpg`
      : `${props.item.title}.mp4`;

  try {
    const response = await axios.get(imageUrl, {
      responseType: "blob",
    });
    const url = window.URL.createObjectURL(new Blob([response.data]));

    const link = document.createElement("a");
    link.href = url;

    link.setAttribute("download", type);
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  } catch (error) {
    console.error("Error downloading:", error);
  }
}
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
    <v-card-actions>
      <v-btn @click="handleDownload" color="orange"> Download </v-btn>
    </v-card-actions>
  </v-card>
</template>
