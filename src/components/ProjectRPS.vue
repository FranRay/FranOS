<template>
  <div ref="head" :style="style" class="window">
    <!-- Title Bar -->
    <div class="title-bar hide">
      <h3>{{ title }}</h3>
      <button @click="$emit('closeRPS')"></button>
    </div>

    <!-- Window Content -->
    <div class="content">
      <div class="intro">
        <h1>Machine Learning RPS</h1>
        <div class="desc">
          <p>An interface and a classification model for rock paper scissor gestures, which will accurately detect and classify the hand gestures of users playing the game.</p>
        </div>
      </div>

      <div class="case">
        <img src="/img/_CODE/RPS/CoverImage.png">
        <br>
        <p>The development process involved creating a user-specific dataset for higher accuracy and using OpenCV library to capture images of rock, paper, scissor, and nothing.</p>
      </div>

      <div class = "flex-grid">
        <img src="/img/_CODE/RPS/Content.png">
        <img src="/img/_CODE/RPS/Content-3.png">
      </div>
      <br>
      <div class = "flex-grid">
        <img src="/img/_CODE/RPS/Content-2.png">
        <img src="/img/_CODE/RPS/Content-1.png">
      </div>
      <div class="case">
        <p>The data was pre-processed by normalizing pixel values and applying data augmentation techniques before training and evaluating the model.</p>
        <br>
        <div class="video">
          <iframe width="100%" height="100%" src="https://www.youtube.com/embed/fs_YU5ppGAM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
        </div>
        <br>
        <p>The trained model achieved a test accuracy of 100%, indicating successful development.</p>
      </div>

    </div>

  </div>
</template>
  
<script setup lang = "ts">
  import { ref } from 'vue';
  import { useDraggable } from '@vueuse/core';

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
      width: 50em;
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
      width: 97.5%;
    }

    .intro {
      display: flex;
      flex-direction: column;
      width: 90%;
      margin-inline: auto;
      margin-top: 2em;

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

    .case {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      margin-block: 2em;
      margin-inline: auto;
      width: 90%;

      img {
        width: 90%;
      }
    }

    .video {
      // padding-top: 56.25%;
      width: 90%;
      aspect-ratio: 16/9;
    }
  }

  //flex grids 
  .flex-grid {
    display: flex;
    width: 80%;
    align-self: center;
    justify-content: space-between;
    img {
      width: 48%;
    }
  }

  .hide {
    display: none;

    @include media(laptop) {
      display: flex;
    }
  }
</style>