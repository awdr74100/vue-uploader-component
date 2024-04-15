<template>
  <div class="flex w-full flex-col items-center justify-center">
    <div class="relative hover:opacity-90">
      <div
        class="flex size-[100px] items-center justify-center overflow-hidden rounded-full border-2 border-gray-500"
      >
        <CameraSvg v-if="!tempUrl" />
        <img v-else :src="tempUrl" class="size-full object-cover" />
      </div>
      <div
        v-if="tempUrl"
        class="absolute bottom-0 right-0 flex size-9 items-center justify-center rounded-full shadow"
      >
        <CameraSvg class="size-5 fill-orange-500" />
      </div>

      <input
        type="file"
        name="file"
        class="absolute inset-0 z-1 size-full cursor-pointer opacity-0"
        @change="handleFileUpload"
      />

      <div class="mt-2.5 text-center">
        <div class="text-base font-medium text-gray-500">123</div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onBeforeUnmount } from 'vue'
import { useVModel } from '@vueuse/core'
import CameraSvg from '@/assets/svg/camera.svg'

const props = defineProps<{
  modelValue: File | null
  src?: string
}>()

const emit = defineEmits(['update:modelValue'])

// props.src 被用作初始值，props 未來更新都不甘他的事
const tempUrl = ref(props.src)

const fileWritable = useVModel(props, 'modelValue', emit)

function handleFileUpload(event: Event) {
  const file = (event.target as HTMLInputElement).files?.[0]

  if (!file) return

  fileWritable.value = file
  tempUrl.value = URL.createObjectURL(file)
}

onBeforeUnmount(() => {
  if (fileWritable.value && tempUrl.value) {
    URL.revokeObjectURL(tempUrl.value)
  }
})
</script>
