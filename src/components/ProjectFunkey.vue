<template>
  <div ref="head" :style="style" class="window">
    <!-- Title Bar -->
    <div class="title-bar hide">
      <h3>{{ title }}</h3>
      <button @click="$emit('closeFunkey')"></button>
    </div>

    <!-- Window Content -->
    <div class="content">
      <div class="intro">
        <h1>Funkey</h1>
        <div class="desc">
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        </div>
      </div>

      <div class="case">
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        <img src="/img/_UXUI/Funkey/StyleGuide.png">
        <br>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        <img src="/img/_UXUI/Funkey/Persona.png">
        <br>
        <!-- Carousel -->
        <Carousel>
          <Slide v-for="slide in slides" :key="slide.id">
            <div class="carousel__item">
              <img :src="`${slide.src}`" />
            </div>
          </Slide>

          <template #addons>
            <Navigation />
            <Pagination />
          </template>
        </Carousel>
        <br>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        <br>
        <img src="/img/_UXUI/Funkey/Storyboard.png">

        <Carousel>
          <Slide v-for="slide in slides2" :key="slide.id">
            <div class="carousel__item">
              <img :src="`${slide.src}`" />
            </div>
          </Slide>

          <template #addons>
            <Navigation />
            <Pagination />
          </template>
        </Carousel>
      </div>

    </div>

  </div>
</template>
  
<script setup lang = "ts">
  import { ref, defineComponent } from 'vue';
  import { useDraggable } from '@vueuse/core';
  import { Carousel, Navigation, Pagination, Slide } from 'vue3-carousel'

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

  // Carousel
  const slides = [
    { id: 1, src: 'img/_UXUI/Funkey/Wireframe.png'},
    { id: 2, src: 'img/_UXUI/Funkey/Wireframe2.png'},
  ]

  const slides2 = [
    { id: 1, src: 'img/_UXUI/Funkey/Prototype.png'},
    { id: 2, src: 'img/_UXUI/Funkey/Prototype1.png'},
    { id: 3, src: 'img/_UXUI/Funkey/Prototype2.png'},
    { id: 4, src: 'img/_UXUI/Funkey/Prototype3.png'},
  ]

  defineComponent({
    name: 'Basic',
    components: {
      Carousel,
      Slide,
      Pagination,
      Navigation,
    },
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

  // carousel
  .carousel__item {
  // min-height: 200px;
  width: 100%;
  background-color: var(--clr-accent);
  color: var(--clr-primary);
  font-size: 20px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  }

  .carousel__slide {
    padding: 5px;
  }

  .carousel__prev,
  .carousel__next {
    box-sizing: content-box;
    color: red;
  }

  .carousel__pagination {
    margin-left: -2.5em;
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

  .hide {
    display: none;

    @include media(laptop) {
      display: flex;
    }
  }
</style>