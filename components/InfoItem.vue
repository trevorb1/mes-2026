<script setup lang="ts">
defineProps<{
  icon: string
  title: string
  subtitle: string
  /** Vertical alignment of the row. Defaults to 'start'. */
  align?: 'start' | 'center'
  /** Icon size. Defaults to 'xl'. */
  iconSize?: 'xl' | '2xl'
  /** Extra classes applied to the title text. */
  titleClass?: string
}>()
</script>

<template>
  <div class="flex gap-4" :class="align === 'center' ? 'items-center' : 'items-start'">
    <div :class="iconSize === '2xl' ? 'text-2xl' : 'text-xl'">{{ icon }}</div>
    <div>
      <div class="font-bold" :class="titleClass">{{ title }}</div>
      <div class="text-sm opacity-70">{{ subtitle }}</div>
    </div>
  </div>
</template>
