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
    <WindowAbout 
      v-if="isOpenAbout" 
      :title="'About Me'" 
      @openAbout="openWindowAbout" 
      @closeAbout="closeWindowAbout"
    />
    <WindowGraphics 
      v-if="isOpenGraphics" 
      :title="'Graphic Design'" 
      @openGraphics="openWindowGraphics" 
      @closeGraphics="closeWindowGraphics" 

      @openChunk="openProjectChunk"
      @openCrab="openProjectCrab"
      @openCiao="openProjectCiao"
    />
    <WindowUXUI 
      v-if="isOpenUXUI" 
      :title="'UX/UI Design'" 
      @openUXUI="openWindowUXUI" 
      @closeUXUI="closeWindowUXUI" 

      @openDL="openProjectDL"
      @openPIHSS="openProjectPIHSS"
      @openSewcial="openProjectSewcial"
    />
    <WindowWorks 
      v-if="isOpenWorks" 
      :title="'Other Works'" 
      @openWorks="openWindowWorks" 
      @closeWorks="closeWindowWorks" 

      @openTwine="openProjectTwine"
      @openHT="openProjectHT"
      @openDS="openProjectDS"

      @openRPS="openProjectRPS"
      @openChickboy="openProjectChickboy"
      @openSewcial="openProjectSewcial"
      @openDL="openProjectDL"
    />

    <!-- Projects -->
    <ProjectChunk
      v-if="isOpenChunk" 
      :title="'Chunk Bakehouse'" 
      @openChunk="openProjectChunk"
      @closeChunk="closeProjectChunk"
    />
    <ProjectCrab
      v-if="isOpenCrab" 
      :title="'Mr. Crab'" 
      @openCrab="openProjectCrab"
      @closeCrab="closeProjectCrab"
    />
    <ProjectCiao
      v-if="isOpenCiao" 
      :title="'Ciao! Pasta'" 
      @openCiao="openProjectCiao"
      @closeCiao="closeProjectCiao"
    />

    <ProjectDL
      v-if="isOpenDL" 
      :title="'DesignLab'" 
      @openDL="openProjectDL"
      @closeDL="closeProjectDL"
    />
    <ProjectPIHSS
      v-if="isOpenPIHSS" 
      :title="'Pakistan Islamia Higher Secondary School'" 
      @openPIHSS="openProjectPIHSS"
      @closePIHSS="closeProjectPIHSS"
    />
    <ProjectSewcial
      v-if="isOpenSewcial" 
      :title="'Sewcial'" 
      @openSewcial="openProjectSewcial"
      @closeSewcial="closeProjectSewcial"
    />

    <ProjectTwine
      v-if="isOpenTwine" 
      :title="'Twine'" 
      @openTwine="openProjectTwine"
      @closeTwine="closeProjectTwine"
    />
    <ProjectHT
      v-if="isOpenHT" 
      :title="'Hypertext'" 
      @openHT="openProjectHT"
      @closeHT="closeProjectHT"
    />
    <ProjectDS
      v-if="isOpenDS" 
      :title="'Digital Storytelling'" 
      @openDS="openProjectDS"
      @closeDS="closeProjectDS"
    />

    <ProjectRPS
      v-if="isOpenRPS" 
      :title="'ML: Rock Paper Scissors'" 
      @openRPS="openProjectRPS"
      @closeRPS="closeProjectRPS"
    />
    <ProjectChickboy
      v-if="isOpenChickboy" 
      :title="'Chickboy'" 
      @openChickboy="openProjectChickboy"
      @closeChickboy="closeProjectChickboy"
    />
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

  // import project windows
  import ProjectChunk from '@/components/ProjectChunk.vue';
  import ProjectCrab from '@/components/ProjectCrab.vue';
  import ProjectCiao from '@/components/ProjectCiao.vue';

  import ProjectFunkey from '@/components/ProjectFunkey.vue';
  import ProjectDL from '@/components/ProjectDL.vue';
  import ProjectPIHSS from '@/components/ProjectPIHSS.vue';
  import ProjectSewcial from '@/components/ProjectSewcial.vue';

  import ProjectTwine from '@/components/ProjectTwine.vue';
  import ProjectHT from '@/components/ProjectHT.vue';
  import ProjectDS from '@/components/ProjectDS.vue';

  import ProjectRPS from '@/components/ProjectRPS.vue';
  import ProjectChickboy from '@/components/ProjectChickboy.vue';

  // --------------- DOCKS ---------------
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
  
  // --------------- MAIN WINDOWS ---------------
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

          isOpenChunk.value = false;
          isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
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

          isOpenChunk.value = false;
          isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
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

          isOpenChunk.value = false;
          isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
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

          isOpenChunk.value = false;
          isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeWindowWorks() {
    isOpenWorks.value = false;
  }

  // --------------- PROJECT WINDOWS ---------------
  // chunk bakehouse
  const isOpenChunk = ref(false);
  function openProjectChunk() {
    switch (isOpenChunk.value) {
      case true: 
        isOpenChunk.value = false;
        break;
      case false:
        isOpenChunk.value = true;
        console.log("running~");
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectChunk() {
    isOpenChunk.value = false;
  }

  // crab
  const isOpenCrab = ref(false);
  function openProjectCrab() {
    switch (isOpenCrab.value) {
      case true: 
        isOpenCrab.value = false;
        break;
      case false:
        isOpenCrab.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

          isOpenChunk.value = false;
          isOpenCiao.value = false;
          isOpenFunkey.value = false;
          isOpenDL.value = false;
          isOpenPIHSS.value = false;
          isOpenSewcial.value = false;
          isOpenTwine.value = false;
          isOpenHT.value = false;
          isOpenDS.value = false;
          isOpenRPS.value = false;
          isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectCrab() {
    isOpenCrab.value = false;
  }

  // ciao
  const isOpenCiao = ref(false);
  function openProjectCiao() {
    switch (isOpenCiao.value) {
      case true: 
        isOpenCiao.value = false;
        break;
      case false:
        isOpenCiao.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenChunk.value = false;
					isOpenCrab.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectCiao() {
    isOpenCiao.value = false;
  }

  // funkey
  const isOpenFunkey = ref(false);
  function openProjectFunkey() {
    switch (isOpenFunkey.value) {
      case true: 
        isOpenFunkey.value = false;
        break;
      case false:
        isOpenFunkey.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenChunk.value = false;
					isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectFunkey() {
    isOpenFunkey.value = false;
  }

  // design lab
  const isOpenDL = ref(false);
  function openProjectDL() {
    switch (isOpenDL.value) {
      case true: 
        isOpenDL.value = false;
        break;
      case false:
        isOpenDL.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenChunk.value = false;
					isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectDL() {
    isOpenDL.value = false;
  }

  // PIHSS
  const isOpenPIHSS = ref(false);
  function openProjectPIHSS() {
    switch (isOpenPIHSS.value) {
      case true: 
        isOpenPIHSS.value = false;
        break;
      case false:
        isOpenPIHSS.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenChunk.value = false;
					isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectPIHSS() {
    isOpenPIHSS.value = false;
  }

  // sewcial
  const isOpenSewcial = ref(false);
  function openProjectSewcial() {
    switch (isOpenSewcial.value) {
      case true: 
        isOpenSewcial.value = false;
        break;
      case false:
        isOpenSewcial.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenChunk.value = false;
					isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectSewcial() {
    isOpenSewcial.value = false;
  }

  // twine
  const isOpenTwine = ref(false);
  function openProjectTwine() {
    switch (isOpenTwine.value) {
      case true: 
        isOpenTwine.value = false;
        break;
      case false:
        isOpenTwine.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenChunk.value = false;
					isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectTwine() {
    isOpenTwine.value = false;
  }

  // hypertext
  const isOpenHT = ref(false);
  function openProjectHT() {
    switch (isOpenHT.value) {
      case true: 
        isOpenHT.value = false;
        break;
      case false:
        isOpenHT.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenChunk.value = false;
					isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectHT() {
    isOpenHT.value = false;
  }

  // digital storytelling
  const isOpenDS = ref(false);
  function openProjectDS() {
    switch (isOpenDS.value) {
      case true: 
        isOpenDS.value = false;
        break;
      case false:
        isOpenDS.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenChunk.value = false;
					isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectDS() {
    isOpenDS.value = false;
  }

  // machine learning
  const isOpenRPS = ref(false);
  function openProjectRPS() {
    switch (isOpenRPS.value) {
      case true: 
        isOpenRPS.value = false;
        break;
      case false:
        isOpenRPS.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenChunk.value = false;
					isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectRPS() {
    isOpenRPS.value = false;
  }

  // chickboy
  const isOpenChickboy = ref(false);
  function openProjectChickboy() {
    switch (isOpenChickboy.value) {
      case true: 
        isOpenChickboy.value = false;
        break;
      case false:
        isOpenChickboy.value = true;
        
        // run this code on mobile-tablet
        if (window.innerWidth <= 768) {
          isOpenAbout.value = false;
          isOpenGraphics.value = false;
          isOpenUXUI.value = false;
          isOpenWorks.value = false;

					isOpenChunk.value = false;
					isOpenCrab.value = false;
					isOpenCiao.value = false;
					isOpenFunkey.value = false;
					isOpenDL.value = false;
					isOpenPIHSS.value = false;
					isOpenSewcial.value = false;
					isOpenTwine.value = false;
					isOpenHT.value = false;
					isOpenDS.value = false;
					isOpenRPS.value = false;
					isOpenChickboy.value = false;
        }
        break;
    }
  }
  function closeProjectChickboy() {
    isOpenChickboy.value = false;
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
