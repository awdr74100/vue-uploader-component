<template>
  <div class="mx-auto max-w-36 mt-10">
    <FileUpload v-model="file" src="https://i.imgur.com/Iz6mnGL.png"/>
    <!-- <div class="w-full flex justify-center items-center">
      <FileUploader />
    </div> -->
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'

import FileUpload from '@/components/FileUpload.vue'
// import FileUploader from '@/components/FileUploader.vue'

const file = ref<File | null>(null)

watch(file, (newFile, oldFile) => {
  console.log(newFile, oldFile)
})
</script>
