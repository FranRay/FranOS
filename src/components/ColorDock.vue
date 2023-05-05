<template class = "color">
      <nav ref={dockRef} className="dock">
        <ul>
          <li className="app" onMouseMove={handleAppHover}>
            <a @click="$emit('open')">
              <img src="../images/icons/C-AboutMe.png"/>
              <span className="tooltip">About Me</span>
            </a>
          </li>
          <li className="app" onMouseMove={handleAppHover}>
            <a href="https://www.frontend.fyi" target="_blank">
              <img src="../images/icons/C-GraphicDesign.png" />
              <span className="tooltip">Graphic Design</span>
            </a>
          </li>
          <li className="app" onMouseMove={handleAppHover}>
            <a href="https://www.frontend.fyi" target="_blank">
              <img src="../images/icons/C-UXUI.png" />
              <span className="tooltip">UX/UI</span>
            </a>
          </li>
          <li className="app" onMouseMove={handleAppHover}>
            <a href="https://www.frontend.fyi" target="_blank">
              <img src="../images/icons/C-OtherWork.png" />
              <span className="tooltip">Other Work</span>
            </a>
          </li>
          <li className="app hide" onMouseMove={handleAppHover}>
            <a href="https://www.linkedin.com/in/franraymundo" target="_blank">
              <img src="../images/icons/C-LinkedIn.png" />
              <span className="tooltip">LinkedIn</span>
            </a>
          </li>
          <li className="app hide" onMouseMove={handleAppHover}>
            <a href="https://www.behance.net/franraymundo" target="_blank">
              <img src="../images/icons/C-Behance.png" />
              <span className="tooltip">Behance</span>
            </a>
          </li>
          <li className="app" onMouseMove={handleAppHover}>
            <a @click="$emit('color-toggle')">
              <img src="../images/icons/C-ToggleTheme.png" />
              <span className="tooltip">Toggle Theme</span>
            </a>
          </li>
        </ul>
      </nav>
</template>
    
<style scoped lang = "scss">
  .dock {
    // overflow: hidden;
    border-bottom: 0px;
    margin: auto auto 1em auto;
    padding: 0px;
    background-color: var(--clr-accent);
    border: 3px solid var(--clr-primary);
    border-radius: 10px;

    @include media(laptop) {
      transform: scale(20px);
      padding: 0 2em;
      margin: auto auto -0.1em auto;
      background-color: var(--clr-accent);
      border: 3px solid var(--clr-primary);
      transform: perspective(10px) rotateX(1.5deg);
    }
  }

  .dock ul {
    display: flex;
    padding-inline: 0px;
    margin-block: 0.5em;
    margin-inline: 2em;
    
    @include media(laptop){
      margin-top: -2.5em;
      list-style-type: none;
      padding: 0;
      transform: perspective(11px) rotateX(-1.5deg);
    } 
  }

  nav {
      .app {
        display: flex;
        transition: width, height, margin-top, cubic-bezier(0.25, 1, 0.5, 1) 100ms;
        width: 60px;
        height: 60px;
        position: relative;

        @include media(laptop) {
          width: 90px;
          height: 90px;
        }

        img {
          height: 100%;
        }

        a {
          display: flex;
          width: 100%;
          height: 100%;
          border-radius: 12px;
          color: var(--clr-text-2);

          justify-content: center;
          align-items: center;
        }
      }

      .app:hover .tooltip,
      .app:focus-within .tooltip {
        opacity: 1;
      }

      .tooltip {
        position: absolute;
        top: -30px;
        left: 50%;
        transform: translateX(-50%);
        opacity: 0;
        transition: ease-in opacity 500ms;
        display: block;
        background: var(--clr-accent);
        padding-inline: 0.75em;
        border-radius: 0.25em;
        height: 1.5em;
        width: auto;
        white-space: nowrap;
      }

      .hide {
        display: none;

        @include media (tablet) {
          display: flex;
        }
      }

      // app animation related
      .app:hover {
        @include media (laptop) {
          width: 90px;
          height: 90px;
          margin-top: -30px;
        }
      }

      /* Right side */
      .app:hover + .app {
        @include media (laptop) {
          transition: 0.2s;
          width: calc(80px + var(--dock-offset-right, 0px));
          height: calc(80px + var(--dock-offset-right, 0px));
          margin-top: calc(-20px + var(--dock-offset-right, 0px) * -1);
        }
      }

      .app:hover + .app + .app {
        @include media (laptop) {
          transition: 0.2s;
          width: calc(70px + var(--dock-offset-right, 0px));
          height: calc(70px + var(--dock-offset-right, 0px));
          margin-top: calc(-10px + var(--dock-offset-right, 0px) * -1);
        }
      }

      /* Left side */
      .app:has(+ .app:hover){
        @include media (laptop) {
          transition: 0.2s;
          width: calc(80px + var(--dock-offset-left, 0px));
          height: calc(80px + var(--dock-offset-left, 0px));
          margin-top: calc(-20px + var(--dock-offset-left, 0px) * -1);
        }
      }

      .app:has(+ .app + .app:hover){
        @include media (laptop) {
          transition: 0.2s;
          width: calc(70px + var(--dock-offset-left, 0px));
          height: calc(70px + var(--dock-offset-left, 0px));
          margin-top: calc(-10px + var(--dock-offset-left, 0px) * -1);
        }
      }
  }
</style>