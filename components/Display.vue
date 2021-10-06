<template>
  <div class="flex flex-wrap justify-center mt-24">
    <div
      v-for="(anime, index) in results"
      :key="index"
      class="m-2 max-w-md p-5 border rounded-md"
    >
      <video :src="anime.video" autoplay loop muted class="mb-6"></video>
      <ul class="text-gray-600 text-sm">
        <li class="mb-2">Filename: {{ anime.filename }}</li>
        <li class="mb-2">Episode: {{ anime.episode || "unknown" }}</li>
        <li class="mb-2">
          Minutes: {{ convertToMinutes(anime.from) }} -
          {{ convertToMinutes(anime.to) }}
        </li>
        <li class="mb-2">
          Similarity: {{ Math.round(anime.similarity * 100) }}%
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Display",
  props: {
    results: {
      type: Array,
      default: {}
    }
  },
  methods: {
    convertToMinutes(number) {
      return (number / 60).toFixed(2).replace(".", ":");
    }
  }
};
</script>

<style scoped>
video {
  width: 400px;
  height: 250px;
  object-fit: cover;
}
</style>
