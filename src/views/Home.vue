<template>
  <body>
    <p>hi guys</p>
    <WindowAbout v-if="isOpen" :title="'About Me'" @open="openWindow" @close="closeWindow" >
      <slot>Hey, I'm trying to figure this out.</slot>
    </WindowAbout>

    <div id="darkdock" class = "dock-container darkdock">
      <DarkDock 
        @open="openWindow"
        @dark-toggle="darkToggle"
      />
    </div>
    <div id="lightdock" class = "dock-container lightdock">
      <LightDock
        @open="openWindow"
        @light-toggle="lightToggle"
      />
    </div>
    <div id="colordock" class = "dock-container colordock">
      <ColorDock
        @open="openWindow"
        @color-toggle="colorToggle"
      />
    </div>
  </body>
</template>

<script setup lang="ts">
  import { ref, computed, onMounted } from 'vue';
  import DarkDock from '@/components/DarkDock.vue';
  import LightDock from '@/components/LightDock.vue';
  import ColorDock from '@/components/ColorDock.vue';
  import WindowAbout from '@/components/WindowAbout.vue';
  import { useDraggable } from '@vueuse/core';

  //dock code
  let darkdock: HTMLElement | null = null;
  let lightdock: HTMLElement | null = null;
  let colordock: HTMLElement | null = null;

  onMounted(() => {
    darkdock = document.getElementById('darkdock');
    lightdock = document.getElementById('lightdock');
    colordock = document.getElementById('colordock');
  });

  function darkToggle() {
    document.documentElement.setAttribute('data-theme', 'light');
    if (darkdock && lightdock && colordock) {
      darkdock.style.display = 'none';
      lightdock.style.display = 'flex';
      colordock.style.display = 'none';
      console.log(lightdock.style.display);
    }
  }
  function lightToggle() {
    document.documentElement.setAttribute('data-theme', 'color');
    if (darkdock && lightdock && colordock) {
      darkdock.style.display = 'none';
      lightdock.style.display = 'none';
      colordock.style.display = 'flex';
      console.log(lightdock.style.display);
    }
  }
  function colorToggle() {
    document.documentElement.setAttribute('data-theme', 'dark');
    if (darkdock && lightdock && colordock) {
      darkdock.style.display = 'flex';
      lightdock.style.display = 'none';
      colordock.style.display = 'none';
      console.log(lightdock.style.display);
    }
  }

  //about window code
  const isOpen = ref(true);

  function openWindow() {
    switch (isOpen.value) {
      case true: 
        isOpen.value = false;
        break;
      case false:
        isOpen.value = true;
        break;
    }
  }

  function closeWindow() {
    isOpen.value = false;
  }
</script>

<style scoped lang = "scss">
  body {
    display: flex;
    flex-direction: column;
  }
  .dock-container {
    font-weight: 700;
    margin-top: auto;
    // display: flex;
  }

  .darkdock {
    display: flex;
  }
  .lightdock {
    display: none;
  }

  .colordock {
    display: none;
  }
</style>
