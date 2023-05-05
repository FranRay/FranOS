<template>
  <div ref="head" :style="style" class="window">
    <div class="title-bar hide">
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
    color: var(--clr-text-2);
    background-color: var(--clr-accent);

    border: 2px solid var(--clr-primary);
    border-radius: 1em;

    width: 100%;
    height: 80%;
    margin-top: 0.5em;
    margin-inline: auto;

    @include media(laptop){
      position: fixed;
      top: 100px;
      left: 100px;
      width: 40em;
      height: 35em;

      
      transition: 120ms;
    }
    

    .title-bar {
      @include media(laptop) {
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 40px;
        padding: 0 10px;

        background-color: var(--clr-secondary);
        color: var(--clr-text-2);

        border-bottom: 2px solid var(--clr-primary);
        border-radius: 1em 1em 0em 0em;
      }
      

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

  .hide {
    display: none;

    @include media(laptop) {
      display: flex;
    }
  }
</style>
  