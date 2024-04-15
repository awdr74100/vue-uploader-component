<template>
  <div
    @dragover.prevent.stop="handleDragOver"
    @dragleave.prevent.stop="handleDragLeave"
    @drop.prevent.stop="handleDrop"
    @click="handleClick"
    class="size-24 bg-gray-100 rounded-full flex justify-center items-center"
  >
    <CameraSvg />
  </div>
  <div>
    <input type="file" class="hidden" ref="fileElement" @change="handleChange" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import CameraSvg from '@/assets/svg/camera.svg'

const fileElement = ref<HTMLInputElement | null>(null)

const dragHover = ref(false)

const handleDragOver = () => {
  console.log('true')
  dragHover.value = true
}

const handleDragLeave = () => {
  console.log('false')
  dragHover.value = false
}

const handleDrop = (e: DragEvent) => {
  const file = e.dataTransfer?.files[0]

  console.log(file)
}

const handleClick = (e: Event) => {
  fileElement.value?.click()
}

const handleChange = (e: Event) => {
  const file = (e.target as HTMLInputElement).files?.[0];

  console.log(file);

  const render = new FileReader();

  // render.addEventListener()


}
</script>
