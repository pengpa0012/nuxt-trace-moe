<template>
  <div>
    <div class="flex justify-center">
      <input
        type="text"
        v-model="imgUrl"
        placeholder="Put image URL here..."
        class="border text-md p-2 mr-2 rounded w-full"
      />
      <button
        class="bg-black text-white rounded py-2 px-8 flex self-center"
        @click="displayAnime"
      >
        Search
      </button>
    </div>
    <h1 v-if="showError" class="text-2xl text-gray-500 mx-auto my-12">
      Please Put a valid URL
    </h1>
    <h1 v-if="loading" class="text-2xl text-gray-500 mx-auto my-12">
      LOADING
    </h1>
    <Display :results="results" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      results: [],
      imgUrl: "",
      showError: false,
      loading: false
    };
  },
  methods: {
    displayAnime() {
      if (this.imgUrl == "") {
        alert("Please put a valid URL");
        return;
      }
      this.results = [];
      this.showError = false;
      this.loading = true;
      fetch(
        `https://api.trace.moe/search?url=${encodeURIComponent(this.imgUrl)}`
      )
        .then(res => res.json())
        .then(data => {
          this.loading = false;
          this.showError = false;
          this.imgUrl = "";
          this.results = [];
          this.results.push(...data.result);
        })
        .catch(err => {
          this.loading = false;
          this.showError = true;
        });
    }
  }
};
</script>
