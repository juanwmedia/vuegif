<template>
  <section class="grid">
    <article
      class="gif"
      v-for="(gif, $index) in gifs"
      :key="$index"
      :style="{ 'background-image': 'url(' + gif + ')' }"
    >
      <a href="#" @click="$emit('selected-gif', gif)" class="gif__link"></a>
    </article>
  </section>
</template>

<script>
export default {
  name: "AppGrid",
  props: {
      gifs: {
          type: Array,
          required: true
      }
  }
};
</script>

<style scoped>
/* Gif grid */
.grid {
  display: grid;
  grid: repeat(auto-fit, minmax(10vmin, 1fr)) / repeat(
      auto-fit,
      minmax(10vmin, 1fr)
    );
  grid-auto-rows: minmax(10vmin, 1fr);
  grid-auto-flow: row dense;
  grid-gap: 1.5rem;
}
.gif {
  border: 1px solid;
}
.gif:first-child {
  grid-row-start: span 3;
  grid-column-start: span 3;
}
.gif:nth-child(2n + 3) {
  grid-row-start: span 3;
}
.gif:nth-child(4n + 5) {
  grid-column-start: span 2;
  grid-row-start: span 2;
}
.gif:nth-child(6n + 7) {
  grid-row-start: span 2;
}
.gif:nth-child(8n + 9) {
  grid-column-start: span 2;
  grid-row-start: span 3;
}
.gif__link {
  display: block;
  height: 100%;
  /* background-image: url("../assets/cat.gif"); */
  background-position: center;
  background-size: cover;
}
</style>
