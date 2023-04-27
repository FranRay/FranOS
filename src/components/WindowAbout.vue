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

  const props = defineProps({
    title: {
      type: String,
      required: true,
    },
  });

  //dragging function
  const head = ref<HTMLElement | null>(null)

  // `style` will be a helper computed for `left: ?px; top: ?px;`
  const { x, y, style } = useDraggable(head, {
    initialValue: { x: 40, y: 40 },
  })
</script>
  
<style scoped>
  .window {
    position: fixed;
    top: 100px;
    left: 100px;
    width: 600px;
    height: 500px;
    color: var(--clr-text-2);
    background-color: var(--clr-accent);
    border-radius: 1em;
  }
  
  .title-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 40px;
    padding: 0 10px;
    background-color: var(--clr-primary);
    color: var(--clr-text-2);
    border-radius: 1em 1em 0em 0em;
  }
  
  .content {
    padding: 10px;
  }

  button {
    all: unset;
    background-color: var(--clr-accent);
    border-radius: 50%;
    height: 1.2em;
    width: 1.2em;
  }
</style>
  