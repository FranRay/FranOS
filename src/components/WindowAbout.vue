<template>
  <div ref="head" :style="style" style="position: fixed" class="window">
    <div class="title-bar">
      <h3>{{ title }}</h3>
      <button @click="$emit('close')"></button>
    </div>
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>
  
<script setup lang = "ts">
  import { ref } from 'vue';
  import { useDraggable } from '@vueuse/core';

  // Heading
  const props = defineProps({
    title: {
      type: String,
      required: true,
    },
  });

  // Dragging function
  const head = ref<HTMLElement | null>(null)
  const { x, y, style } = useDraggable(head, {
    initialValue: { x: 40, y: 40 },
  })
</script>
  
<style scoped lang = "scss">
  .window {
    position: fixed;
    top: 100px;
    left: 100px;
    width: 600px;
    height: 500px;

    color: var(--clr-text-2);
    background-color: var(--clr-accent);

    border: 2px solid var(--clr-primary);
    border-radius: 1em;
    transition: 120ms;

    .title-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: 40px;
      padding: 0 10px;

      background-color: var(--clr-secondary);
      color: var(--clr-text-2);

      border-bottom: 2px solid var(--clr-primary);
      border-radius: 1em 1em 0em 0em;

      button {
        all: unset;
        background-color: var(--clr-secondary);
        border: 2px solid var(--clr-primary);
        border-radius: 50%;
        height: 1.2em;
        width: 1.2em;
      }

      button:hover {
        background-color: var(--clr-primary);
      }
    }

    .content {
      padding: 10px;
    }
  }
</style>
  