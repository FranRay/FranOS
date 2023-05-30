<template>
  <body>
    <svg class="logo" width="1020" height="210" viewBox="0 0 1020 210" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path fill-rule="evenodd" clip-rule="evenodd" d="M671.004 168.321C677.163 184.874 682.071 198.636 685.728 209.608H760.505L679.088 9.28687e-05H572.84L492 209.608H564.468L578.903 168.321H671.004ZM625.88 57.7437C625.88 78.7118 608.882 95.7097 587.914 95.7097C608.882 95.7097 625.88 112.708 625.88 133.676C625.88 112.708 642.878 95.7097 663.846 95.7097C642.878 95.7097 625.88 78.7118 625.88 57.7437Z" fill="var(--clr-logo)"/>
      <path d="M1019.54 0.288712C1018.19 32.8173 1017.51 67.6557 1017.51 104.804C1017.51 142.144 1018.19 177.079 1019.54 209.608H916.175L846.306 51.9688L851.503 209.608H777.303C778.843 172.267 779.613 137.332 779.613 104.804C779.613 72.4676 778.843 37.6293 777.303 0.288712H883.55L953.708 162.258L948.8 0.288712H1019.54Z" fill="var(--clr-logo)"/>
      <path d="M225.198 53.9898H68.1369V84.305C77.9532 84.4974 92.6777 84.5937 112.31 84.5937C146.186 84.5937 180.64 84.0163 215.671 82.8614V139.45C180.64 138.102 143.684 137.429 104.804 137.429C88.6357 137.429 76.4134 137.525 68.1369 137.717V209.608H0C1.53982 172.267 2.30972 137.332 2.30972 104.804C2.30972 72.2752 1.53982 37.3406 0 0H225.198V53.9898Z" fill="var(--clr-logo)"/>
      <path d="M480.236 69.8692C480.236 86.6147 476.097 100.762 467.821 112.31C459.737 123.859 445.782 132.232 425.957 137.429C428.267 140.508 429.903 142.914 430.865 144.647L477.637 209.608H399.107C390.638 193.824 377.26 171.497 358.975 142.626H316.534V209.608H248.397C249.937 172.267 250.707 137.332 250.707 104.804C250.707 72.2752 249.937 37.3406 248.397 0H316.534V0.288712H375.721C414.601 0.288712 441.74 6.54422 457.138 19.0552C472.537 31.5662 480.236 48.5042 480.236 69.8692ZM316.534 55.7221V88.6357H355.51C371.871 88.6357 384.19 88.1545 392.466 87.1921C400.935 86.0373 406.806 84.305 410.078 81.9952C413.35 79.6855 414.986 76.3172 414.986 71.8902C414.986 67.6557 413.446 64.3836 410.366 62.0739C407.287 59.7641 401.512 58.1281 393.043 57.1657C384.574 56.2033 372.063 55.7221 355.51 55.7221H316.534Z" 
        fill="var(--clr-logo)"/>
    </svg>

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

    .logo {
      display: none;

      @include media(laptop) {
        display: block;
        margin: auto;
        width: 60%;
      }
    }
  }
  .dock-container {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: 700;
  }

  .darkdock {
    display: none;
  }
  .lightdock {
    display: none;
  }

  .colordock {
    display: flex;
  }
</style>
