<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  src: string
  alt: string
  /** Plain-text caption. For HTML captions use the default slot instead. */
  caption?: string
  /** Classes applied to the wrapping div. Defaults to 'px-4 py-4 rounded-2xl'. */
  wrapperClass?: string
  /** Classes applied to the <img> element. Defaults to 'object-contain rounded-xl'. */
  imgClass?: string
  /** Extra classes applied to the caption element. */
  captionClass?: string
}>()

// Eagerly import all assets so Vite processes them through its pipeline.
// This ensures paths are base-aware when deployed to a subpath (e.g. GitHub Pages).
const assets = import.meta.glob('../assets/**/*', { eager: true, import: 'default' }) as Record<string, string>

const resolvedSrc = computed(() => {
  // Normalise './assets/...' → '../assets/...'
  const key = props.src.replace(/^\.?\/assets\//, '../assets/')
  return assets[key] ?? props.src
})
</script>

<template>
  <div :class="wrapperClass ?? 'px-4 py-4 rounded-2xl'">
    <img
      :src="resolvedSrc"
      :alt="alt"
      class="w-full"
      :class="imgClass ?? 'object-contain rounded-xl'"
    />
  </div>
  <div
    class="text-center text-[11px] opacity-40 uppercase tracking-widest mt-2"
    :class="captionClass"
  >
    <slot>{{ caption }}</slot>
  </div>
</template>
