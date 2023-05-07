<template>
  <div ref="head" :style="style" class="window">
    <!-- Title Bar -->
    <div class="title-bar hide">
      <h3>{{ title }}</h3>
      <button @click="$emit('closeGraphics')"></button>
    </div>

    <!-- Window Content -->
    <div class="content">
      <div class="intro">
        <h1>Graphic Design</h1>
        <div class="desc">
          <p>A collection of graphic design projects during the course of my career and education.</p>
        </div>
      </div>

      <!-- grid here -->
      <div class = "container">
      <div class="grid-container">
        <!-- insert grid item - component for card? -->
        <Card @click="$emit('openChunk')" @touchstart="$emit('openChunk')"
          :image="'https://via.placeholder.com/800x600'" 
          :title="'Project 1'">
        </Card>
        <Card @click="$emit('openCrab')" @touchstart="$emit('openCrab')"
          :image="'https://via.placeholder.com/800x600'" 
          :title="'Project 2'">
        </Card>
        <Card @click="$emit('openCiao')" @touchstart="$emit('openCiao')"
          :image="'https://via.placeholder.com/800x600'" 
          :title="'Project 3'">
        </Card>
      </div>
      </div>
      
    </div>

  </div>
</template>
  
<script setup lang = "ts">
  import { ref } from 'vue';
  import { useDraggable } from '@vueuse/core';
  import Card from './Card.vue';

  // Heading Prop
  const props = defineProps({
    title: {
      type: String,
      required: true,
    },
  });

  // Dragging function
  const head = ref<HTMLElement | null>(null)
  const { x, y, style } = useDraggable(head, {
    initialValue: { x: 60, y: 60 },
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
    display: flex;
    flex-direction: column;

    @include media(laptop){
      position: fixed;
      width: 60em;
      height: 35em;
      transition: 120ms;
    }
    
    .title-bar {
      @include media(laptop) {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: fit-width;
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
  }

  .content {
    padding: 10px;
    font-size: 125%;
    overflow-y: scroll;
    overflow-x: hidden;
    height: 100%;

    display:  flex;
    flex-direction: column;
    
    @include media(tablet) {
      width: 98%;
    }

    @include media(laptop) {
      width: 98%;
    }

    .intro {
      width: 90%;
      margin-inline: auto;
      margin-top: 2em;
      display: flex;
      flex-direction: column;

      @include media(laptop) {
        flex-direction: row;
      }
      h1 {
        font-size: clamp(50px, 5.5vmax, 120px);
        line-height: 100%;
      }

      .desc {
        p {
          margin-block: 1em;
        }
      }
    }

    .container {
      width: 90%;
      margin-inline: auto;
      margin-block: 2em;
    }

    .grid-container {
      display: grid;
      grid-template-columns: repeat(1fr);
      grid-template-rows: repeat(1fr);
      grid-column-gap: 1em;
      grid-row-gap: 1em;

      @include media(tablet) {
        grid-template-columns: repeat(2, 1fr);
      }
    }
  }

  .hide {
    display: none;

    @include media(laptop) {
      display: flex;
    }
  }
</style>
  