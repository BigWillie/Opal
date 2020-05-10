<template>
  <div id="app">
    <div class="flex mb-4">
      <div class="w-1/2 h-12 p-12">
          <toggle-wrapper @toggle-wrapper-state-change="setToggleWrapperState($event)" :on="toggleWrapperState" toggle-label="This is my label"></toggle-wrapper>
      </div>
      <div class="w-1/2 h-12 p-12"></div>
    </div>
  </div>
</template>

<script>
import ToggleWrapper from './components/ToggleWrapper.vue'

// Main App component. Contains examples.
export default {
  name: 'App',
  components: {
    ToggleWrapper
  },
  data () {
    return {
      toggleState: false
    }
  },
  methods: {
    // @vuese
    // Receives emitted `toggler-wrapper-state-change` from `ToggleWrapper` component. Updates `toggleWrapperState`
    setToggleWrapperState (toggleState) {
      this.toggleState = toggleState
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
