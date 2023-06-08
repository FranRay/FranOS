<template>
  <div ref="head" :style="style" class="window">
    <!-- Title Bar -->
    <div class="title-bar hide">
      <h3>{{ title }}</h3>
      <button @click="$emit('closeSewcial')"></button>
    </div>

    <!-- Window Content -->
    <div class="content">
      <div class="intro">
        <h1>Sewcial</h1>
        <div class="desc">
          <p>A web design and graphic design project for Sewcial:  a concept that combines sewing and community, a gathering space where people can connect, create, and foster a sense of belonging.</p>
        </div>
      </div>

      <div class="case">
        <img src="/img/_UXUI/Sewcial/SDLC.png">
        <br>
        <img src="/img/_UXUI/Sewcial/ProjectRoadmap.png">
        <br>
        <p>The project followed the agility SDLC method, and was backed by audience research.</p>
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
        <p>Several steps were taken to ensure the design process was smooth, especially establishing guidelines, and creating maps and wireframes.</p>
        <!-- Carousel -->
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
        <br>
        <img src="/img/_UXUI/Sewcial/Sitemap.png">
        <br>
        <img src="/img/_UXUI/Sewcial/Wireframes.png">
        <br>
        <p>Some examples of the final prototype:</p>
        
        <!-- Carousel -->
        <Carousel>
          <Slide v-for="slide in slides3" :key="slide.id">
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
        <p>The prototypes in action: <a href="https://sewcial.space">sewcial.space</a></p>
        <br>
        <p>The project also involved designing and creating a 3D Model, as well as several marketing materials.</p>
        <br>
        <img src="/img/_UXUI/Sewcial/3D.png">
        <br>
        <img src="/img/_UXUI/Sewcial/SocialMedia.png">
        <!-- Carousel -->
        <Carousel>
          <Slide v-for="slide in slides4" :key="slide.id">
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

  import 'vue3-carousel/dist/carousel.css'

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
    { id: 1, src: 'img/_UXUI/Sewcial/EmpathyMap.png'},
    { id: 2, src: 'img/_UXUI/Sewcial/Persona.png'},
    { id: 3, src: 'img/_UXUI/Sewcial/Survey.png'},
  ]

  const slides2 = [
    { id: 1, src: 'img/_UXUI/Sewcial/StyleGuide.png'},
    { id: 2, src: 'img/_UXUI/Sewcial/Sizing2.png'},
  ]

  const slides3 = [
    { id: 1, src: 'img/_UXUI/Sewcial/AboutTemplateEventsBooking.png'},
    { id: 2, src: 'img/_UXUI/Sewcial/CatalogueItemLiked.png'},
    { id: 3, src: 'img/_UXUI/Sewcial/HomeBooking.png'},
  ]

  const slides4 = [
    { id: 1, src: 'img/_UXUI/Sewcial/Poster.png'},
    { id: 2, src: 'img/_UXUI/Sewcial/Tote.png'},
    { id: 3, src: 'img/_UXUI/Sewcial/ClothesTags.png'},
    { id: 4, src: 'img/_UXUI/Sewcial/Stickers.png'},
    { id: 5, src: 'img/_UXUI/Sewcial/Paperbag.png'},
    { id: 6, src: 'img/_UXUI/Sewcial/Pins.png'},
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

  .hide {
    display: none;

    @include media(laptop) {
      display: flex;
    }
  }
</style>