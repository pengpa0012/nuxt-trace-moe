<template>
  <div>
    <div class="flex justify-center py-24 text-gray-600">
      <nuxt-link
        to="search-by-upload"
        class="mr-3 border p-5 rounded-md flex flex-col items-center hover:bg-gray-100"
      >
        <img src="../assets/upload.svg" class="w-32" />
        <span>Search by Upload</span>
      </nuxt-link>
      <nuxt-link
        to="search-by-url"
        class="ml-3 border p-5 rounded-md flex flex-col items-center hover:bg-gray-100"
      >
        <img src="../assets/url.svg" class="w-32" />
        <span>Search by URL</span>
      </nuxt-link>
    </div>
  </div>
</template>
