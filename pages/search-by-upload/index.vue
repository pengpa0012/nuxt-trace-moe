<template>
  <div>
    <div class="flex justify-center flex-col">
      <!-- <div class="button-wrapper">
        <span class="label">
          Upload File
        </span>
        <input
          type="file"
          name="upload"
          id="upload"
          class="upload-box"
          placeholder="Upload File"
          @change="uploadFile"
        />
      </div> -->
      <UploadImages
        :max="1"
        maxError="Max files exceed"
        fileError="images files only accepted"
        clearAll=" "
        class="w-32"
        @changed="uploadFile"
      />
      <h1 v-if="showError" class="text-2xl text-gray-500 mx-auto my-12">
        Please Put a valid FILE
      </h1>
      <h1 v-if="loading" class="text-2xl text-gray-500 mx-auto my-12">
        LOADING
      </h1>
      <Display :results="results" />
    </div>
  </div>
</template>

<script>
import UploadImages from "vue-upload-drop-images";
export default {
  components: {
    UploadImages
  },
  data() {
    return {
      results: [],
      imgUrl: "",
      showError: false,
      loading: false
    };
  },
  methods: {
    uploadFile(files) {
      if (files[0] == null) {
        this.results = [];
        return;
      }
      this.loading = true;
      this.showError = false;
      // For web browsers only
      const formData = new FormData();
      formData.append("image", files[0]);
      fetch("https://api.trace.moe/search", {
        method: "POST",
        body: formData
      })
        .then(res => res.json())
        .then(data => {
          this.loading = false;
          this.showError = false;
          /*  if (this.imgUrl == "") alert("please put a URL"); */
          /* this.imgUrl = ""; */
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

<style scoped>
.container {
  max-width: 250px;
  width: 100%;
  margin: 0 auto;
}
</style>
