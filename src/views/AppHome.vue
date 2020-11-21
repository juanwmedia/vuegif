<template>
  <main>
    <!-- Modal -->
    <article v-show="selectedGif" class="modal">
      <a href="#" class=" modal__close" @click="selectedGif = ''">Close</a>
      <img :src="selectedGif" alt="" class="modal__image" />
    </article>
    <!-- End of Modal -->

    <!-- Header search bar -->
    <AppHeader @search-gifs="searchGifs" @clear-search="clearSearch" />
    <!-- End of header search bar -->

    <!-- Gif grid -->
    <AppGrid :gifs="gifs" @selected-gif="selectGif" />
    <!-- End of Gif grid -->
  </main>

  <hr />
  <pre>{{ $data }}</pre>
</template>

<script>
import { ref, computed } from "vue";
import AppHeader from "@/components/AppHeader.vue";
import AppGrid from "@/components/AppGrid.vue";
export default {
  name: "AppHome",
  setup() {
    const APIkey = ref("fp3zVbJgPQMGYc8FfV27sei2K7wtcQrg");
    const searchTerm = ref("");
    const selectedGif = ref("");
    const gifs = ref([]);

    const APIendpoint = computed(
      () =>
        `https://api.giphy.com/v1/gifs/search?api_key=${APIkey.value}&q=${searchTerm.value}&limit=25&offset=0&rating=g&lang=en`
    );

    async function searchGifs(search) {
      searchTerm.value = search;
      try {
        const request = await fetch(APIendpoint.value);
        const { data } = await request.json();
        gifs.value = data.map(function(gif) {
          return gif.images.downsized.url;
        });
      } catch (error) {
        console.error(error.message);
      }
    }

    function selectGif(gif) {
        selectedGif.value = gif;
    }

    function clearSearch() {
        searchTerm.value = "";
        gifs.value = [];
    }
    return { APIkey, searchTerm, selectedGif, gifs, APIendpoint, searchGifs, selectGif, clearSearch };
  },
  // Options API
  //   data() {
  //     return {
  //       APIkey: "fp3zVbJgPQMGYc8FfV27sei2K7wtcQrg",
  //       searchTerm: "",
  //       selectedGif: "",
  //       gifs: [],
  //     };
  //   },
  //   methods: {
  //     selectGif(gif) {
  //         this.selectedGif = gif;
  //     },
  //     async searchGifs(searchTerm) {
  //       this.searchTerm = searchTerm;
  //       try {
  //         const request = await fetch(this.APIendpoint);
  //         const { data } = await request.json();
  //         this.gifs = data.map(function(gif) {
  //           return gif.images.downsized.url;
  //         });
  //       } catch (error) {
  //         console.error(error.message);
  //       }
  //     },
  //     clearSearch() {
  //       this.searchTerm = "";
  //       this.gifs = [];
  //     },
  //   },
  //   computed: {
  //     APIendpoint() {
  //       return `https://api.giphy.com/v1/gifs/search?api_key=${this.APIkey}&q=${this.searchTerm}&limit=25&offset=0&rating=g&lang=en`;
  //     },
  //   },
  components: {
    AppHeader,
    AppGrid,
  },
};
</script>

<style scoped>
/* Main */
main {
  width: 80%;
  padding: 2rem;
  background-color: lightgray;
  margin: 0 auto;
}
.main--fixed {
  height: 100vh;
  overflow-y: hidden;
}

/* Modal */
.modal {
  display: flex;
  position: absolute;
  justify-content: center;
  align-items: center;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.9);
}

.modal__image {
  width: 75vh;
  height: auto;
  border: 1rem solid white;
}
.modal__close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  color: white;
  text-decoration: none;
}
</style>
