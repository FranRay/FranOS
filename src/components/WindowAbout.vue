<template>
  <div ref="head" :style="style" class="window">
    <!-- Title Bar -->
    <div class="title-bar hide">
      <h3>{{ title }}</h3>
      <button @click="$emit('closeAbout')"></button>
    </div>

    <!-- Window Content -->
    <div class="content">
      <div class="intro">
        <img src="../images/Me-wave.png">

        <div class="intro-text">
          <h1>I'm Fran Raymundo,</h1>
          <div class = "typing">
            <span class = "text_1 role">Interdisciplinary Designer</span>
            <span class = "text_2 role">Creative Technologist</span>
          </div>
          <h1>Based in Dubai</h1>
        </div>

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
    display: flex;
    flex-direction: column;

    @include media(laptop){
      position: fixed;
      width: 40em;
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

    .content {
      padding: 10px;
      font-size: 125%;
      overflow-y: scroll;
      overflow-x: hidden;
      height: 100%;

      display:  flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      @include media(tablet) {
        flex-direction: row-reverse;
        width: 98%;
      }

      @include media(laptop) {
        width: 97%;
      }

      .intro {
        display:  flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 100%;

        @include media(tablet) {
          flex-direction: row-reverse;
          width: 90%;
        }

        // Image
        img {
          width: 75%;

          @include media(tablet) {
            width: 50%;
          }

          @include media(laptop) {
            width: 40%;
          }
        }

        // Intro Text
        .intro-text {
          width: 100%;
          display: flex;
          flex-direction: column;
          justify-content: center;
          align-items: center;

          @include media(tablet) {
            width: 50%;
            margin-left: 2em;
          }

          h1 {
              color: var(--clr-text-2);
              font-size: 1em;

              @include media(tablet) {
                font-size: 1.25em;
              }
          }

          .typing {
            margin-bottom: -5px;
            .role {
              color: var(--clr-text-1);
              padding: 0px;
              font-size: 1em;
              
              @include media(tablet) {
                font-size: 1.25em;
              }
            }

            .text_1 {
              animation: text1;
            }

            .text_2 {
              animation: text2;
            }

            .text_1, .text_2 {
              overflow: hidden;
              white-space: nowrap;
              display: inline-block;
              position: relative;
              animation-duration: 20s;
              animation-timing-function: steps(25, end);
              animation-iteration-count: infinite;
            }

            .text_1::after, .text_2::after {
              content: "|";
              position: absolute;
              right: 0;
              animation: caret infinite;
              animation-duration: 1s;
              animation-timing-function: steps(1, end);
            }

            @keyframes text2 {
              0%, 50%, 100% {
                width: 0;
              }
              
              60%, 90% {
                width: 11em;
              }
            }

            @keyframes text1 {
              0%, 50%, 100% {
                width: 0;
              }
              10%, 40% {
                width: 12.7em;
              }
            }

            @keyframes caret {
              0%, 100% {
                opacity: 0;
              }
              50% {
                opacity: 1;
              }
            }
          }
        }
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
  