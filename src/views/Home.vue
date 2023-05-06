<template>
  <body>
    <!-- Docks -->
    <div id="darkdock" class = "dock-container darkdock">
      <DarkDock 
        @openAbout="openWindowAbout"
        @openGraphics="openWindowGraphics"
        @openUXUI="openWindowUXUI"
        @openWorks="openWindowWorks"
        @dark-toggle="darkToggle"
      />
    </div>
    <div id="lightdock" class = "dock-container lightdock">
      <LightDock
        @openAbout="openWindowAbout"
        @openGraphics="openWindowGraphics"
        @openUXUI="openWindowUXUI"
        @openWorks="openWindowWorks"
        @light-toggle="lightToggle"
      />
    </div>
    <div id="colordock" class = "dock-container colordock">
      <ColorDock
        @openAbout="openWindowAbout"
        @openGraphics="openWindowGraphics"
        @openUXUI="openWindowUXUI"
        @openWorks="openWindowWorks"
        @color-toggle="colorToggle"
      />
    </div>

    <!-- Windows -->
    <WindowAbout class = "window" v-if="isOpenAbout" :title="'About Me'" @openAbout="openWindowAbout" @closeAbout="closeWindowAbout" />
    <WindowGraphics class = "window" v-if="isOpenGraphics" :title="'Graphic Design'" @openGraphics="openWindowGraphics" @closeGraphics="closeWindowGraphics" />
    <WindowUXUI class = "window" v-if="isOpenUXUI" :title="'UX / UI'" @openUXUI="openWindowUXUI" @closeUXUI="closeWindowUXUI" />
    <WindowWorks class = "window" v-if="isOpenWorks" :title="'Other Works'" @openWorks="openWindowWorks" @closeWorks="closeWindowWorks" />
  
  </body>
</template>

<script setup lang="ts">
  import { ref, computed, onMounted, watchEffect } from 'vue';
  import { useDraggable } from '@vueuse/core';

  // import docks
  import DarkDock from '@/components/DarkDock.vue';
  import LightDock from '@/components/LightDock.vue';
  import ColorDock from '@/components/ColorDock.vue';

  // import main windows
  import WindowAbout from '@/components/WindowAbout.vue';
  import WindowGraphics from '@/components/WindowGraphics.vue';
  import WindowUXUI from '@/components/WindowUXUI.vue';
  import WindowWorks from '@/components/WindowWorks.vue';

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
    }
  }
  function lightToggle() {
    document.documentElement.setAttribute('data-theme', 'color');
    if (darkdock && lightdock && colordock) {
      darkdock.style.display = 'none';
      lightdock.style.display = 'none';
      colordock.style.display = 'flex';
    }
  }
  function colorToggle() {
    document.documentElement.setAttribute('data-theme', 'dark');
    if (darkdock && lightdock && colordock) {
      darkdock.style.display = 'flex';
      lightdock.style.display = 'none';
      colordock.style.display = 'none';
    }
  }
  
  // ---------------MAIN WINDOWS---------------
  // about me window
  const isOpenAbout = ref(true);

  function openWindowAbout() {
    switch (isOpenAbout.value) {
      case true: 
        isOpenAbout.value = false;
        break;
      case false:
        isOpenAbout.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;
        }
        break;
    }
  }

  function closeWindowAbout() {
    isOpenAbout.value = false;
  }

  // graphic design window
  const isOpenGraphics = ref(false);

  function openWindowGraphics() {
    switch (isOpenGraphics.value) {
      case true: 
        isOpenGraphics.value = false;
        break;
      case false:
        isOpenGraphics.value = true;

        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;
        }
        break;
    }
  }

  function closeWindowGraphics() {
    isOpenGraphics.value = false;
  }

  // ux ui window
  const isOpenUXUI = ref(false);

  function openWindowUXUI() {
    switch (isOpenUXUI.value) {
      case true: 
        isOpenUXUI.value = false;
        break;
      case false:
        isOpenUXUI.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenWorks.value = false;
        }
        break;
    }
  }

  function closeWindowUXUI() {
    isOpenUXUI.value = false;
  }

  // other works window
  const isOpenWorks = ref(false);

  function openWindowWorks() {
    switch (isOpenWorks.value) {
      case true: 
        isOpenWorks.value = false;
        break;
      case false:
        isOpenWorks.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
        }
        break;
    }
  }

  function closeWindowWorks() {
    isOpenWorks.value = false;
  }


</script>

<style scoped lang = "scss">
  body {
    display: flex;
    flex-direction: column;
  }
  .dock-container {
    position: absolute;
    top: 0px;
    bottom: 0px;
    left: 0px;
    right: 0px;

    font-weight: 700;
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
