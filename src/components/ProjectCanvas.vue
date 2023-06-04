<template>
    <div ref="head" :style="style" class="window">
      <!-- Title Bar -->
      <div class="title-bar hide">
        <h3>{{ title }}</h3>
        <button @click="$emit('closeCanvas')"></button>
      </div>
  
      <!-- Window Content -->
      <div class="content">
        <div class="intro">
          <h1>Marceline's Escape</h1>
          <div class="desc">
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
          </div>
        </div>
  
        <div class="case">
          <img src="/img/_CODE/Canvas/CoverImage.png">
          <br>
          <p>One was to tell the story of Cinderella in ways more than one: a mix of mellow, surprising, and harsh endings, as well as the original ending. I  wanted the users to still experience the fairytale, but with a broader perspective, and different endings depending on their decisions. The second goal was to ensure that the audience felt their involvement in the story, and I intended for that to be accomplished through the multiple choices and endings.</p>
        </div>

        <div class = "flex-grid">
          <img src="/img/_CODE/Canvas/Content1.png">
          <img src="/img/_CODE/Canvas/Content4.png">
        </div>
        <br>
        <div class = "flex-grid">
          <img src="/img/_CODE/Canvas/Content3.png">
          <img src="/img/_CODE/Canvas/Content2.png">
        </div>
        <div class="case">
          <p>Apart from achieving these goals, there was something else in this story's creation that I found difficult yet enjoyable, and that was the production of the hand drawn images throughout the twine. The process was very long, yet ultimately rewarding, and I am proud of its outcome.</p>
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