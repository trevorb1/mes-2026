<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  href: string
  src: string
  alt: string
  /**
   * Logo size preset:
   *   sm  → h-8  (e.g. EPRI / EIA / NLR inline row)
   *   md  → h-10 (e.g. ResStock / ComStock)  [default]
   *   lg  → h-16 (e.g. ISO-NE / PUDL / EFS)
   *   xl  → h-20 (e.g. EIA Annual Energy Outlook)
   */
  size?: 'sm' | 'md' | 'lg' | 'xl'
}>()

const assets = import.meta.glob('../assets/**/*', { eager: true, import: 'default' }) as Record<string, string>

const resolvedSrc = computed(() => {
  const key = props.src.replace(/^\.?\/assets\//, '../assets/')
  return assets[key] ?? props.src
})
</script>

<template>
  <a :href="href" target="_blank" class="transition-transform hover:scale-110">
    <img
      :src="resolvedSrc"
      :alt="alt"
      class="bg-white border border-gray-100 object-contain"
      :class="{
        'h-8  px-3 py-1 rounded    shadow-sm': size === 'sm',
        'h-10 px-3      rounded    shadow-sm': !size || size === 'md',
        'h-16 px-4 py-2 rounded-lg shadow-md': size === 'lg',
        'h-20 px-4 py-2 rounded-lg shadow-md': size === 'xl',
      }"
    />
  </a>
</template>
