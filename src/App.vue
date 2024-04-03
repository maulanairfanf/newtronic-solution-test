<script setup>
import axios from "axios";
import { onMounted, ref, reactive } from "vue";
import Hero from "./components/Hero.vue";
import Playlist from "./components/Playlist.vue";
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";

const logo = ref("");
const listPlaylist = ref([]);
const isLoading = ref(true);

const heroSection = reactive({
  title: "",
  description: "",
  banner: "",
});

async function fetchApi() {
  isLoading.value = true;
  try {
    const response = await axios.get(
      "http://103.183.75.112/api/directory/dataList"
    );
    if (response) {
      handleData(response.data.data[0]);
      console.log("response: ", response.data.data[0]);
    }
  } catch (error) {
    console.log("error: ", error);
  }
  isLoading.value = false;
}

function handleData(payload) {
  logo.value = payload.logo;
  heroSection.title = payload.title;
  heroSection.description = payload.description;
  heroSection.banner = payload.banner;
  listPlaylist.value = payload.playlist;
}

onMounted(async () => {
  await fetchApi();
});
</script>

<template>
  <v-app>
    <div v-if="isLoading">IsLoading...</div>
    <div v-else>
      <Navbar :logo="logo" />
      <v-main>
        <Hero
          :title="heroSection.title"
          :description="heroSection.description"
          :banner="heroSection.banner"
        />
        <Playlist :listPlaylist="listPlaylist" />
      </v-main>
      <Footer />
    </div>
  </v-app>
</template>
