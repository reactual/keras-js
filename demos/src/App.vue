<template>
  <div id="app" class="container">
    <div class="columns">
      <div class="column is-3" style="min-width: 350px; max-width: 450px;">
        <main-menu :currentView="currentView"></main-menu>
        <info-panel :currentView="currentView"></info-panel>
      </div>
      <div class="column is-9">
        <router-view :hasWebGL="hasWebGL"></router-view>
      </div>
    </div>
  </div>
</template>

<script>
import MainMenu from './components/MainMenu'
import InfoPanel from './components/InfoPanel'

export default {
  components: { MainMenu, InfoPanel },
  data: function() {
    return { hasWebGL: true }
  },
  computed: {
    currentView: function() {
      const path = this.$route.path
      return path.replace(/^\//, '') || 'home'
    }
  },
  created: function() {
    const canvas = document.createElement('canvas')
    const gl = canvas.getContext('webgl2')
    if (gl && gl instanceof window.WebGL2RenderingContext) {
      this.hasWebGL = true
    } else {
      this.hasWebGL = false
    }
  }
}
</script>

<style>
@import 'https://fonts.googleapis.com/css?family=Open+Sans';
@import 'https://fonts.googleapis.com/css?family=Share+Tech+Mono';
@import 'https://fonts.googleapis.com/css?family=Nothing+You+Could+Do';

@import './variables.css';

html {
  background: #CCCCCC;
}

body {
  background: linear-gradient(0deg, #CCCCCC, #F0F0F0);
  color: var(--color-darkgray);
  min-height: 100vh;
  font-family: var(--font-sans-serif);
}

.title {
  width: 100%;
  display: flex;
  flex-direction: row;
  align-items: center;

  & span {
    color: var(--color-green);
    margin-right: 20px;
  }
}

.subtitle {
  color: var(--color-darkgray);
}

.demo {
  padding: 30px;

  & .loading-progress {
    position: absolute;
    top: 0;
    right: 0;
    padding: 30px;
    color: var(--color-green);
    font-size: 18px;
    font-family: var(--font-monospace);
    padding: 20px 50px;
    margin: 30px;
    background: rgba(255, 255, 255, 0.9);
    border-radius: 10px;
  }
}

/****************************************************************/
/* MDL overrides */

.mdl-switch__label {
  font-size: 14px !important;
  color: #69707a;
}

.mdl-switch.is-checked {
  & .mdl-switch__thumb {
    background: var(--color-green-light);
  }

  & .mdl-switch__track {
    background: var(--color-green-lighter);
  }
}

.mdl-textfield {
  & .mdl-textfield__input {
    color: var(--color-darkgray);
    border-bottom-color: var(--color-green-light);
    font-family: var(--font-monospace);
    font-size: 14px !important;
    outline: none;
  }

  & .mdl-textfield__label {
    font-family: var(--font-monospace);
    color: var(--color-green-light);
  }

  & .mdl-icon-toggle__label {
    color: var(--color-green-light);
  }
}

.mdl-textfield.is-focused {
  & .mdl-textfield__input {
    border-color: var(--color-green);
  }

  & .mdl-textfield__label {
    color: var(--color-green);

    &::after {
      background-color: var(--color-green);
    }
  }

  & .mdl-icon-toggle__label {
    color: var(--color-green);
  }
}

.mdl-menu {
  & .mdl-menu__item {
    font-family: var(--font-monospace);
    font-size: 14px !important;
    color: var(--color-lightgray);
    height: 32px;
    line-height: 32px;

    &:hover {
      background-color: var(--color-green-light);
      color: whitesmoke;
    }
  }
}
</style>
