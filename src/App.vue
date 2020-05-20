<template>
  <div id="app">
    <div class="flex mb-4">
      <div class="w-1/2 h-12 p-12">
          <toggle-wrapper @toggle-wrapper-state-change="setToggleWrapperState($event)" :on="toggleWrapperState" label="This is my label"></toggle-wrapper>
      </div>
      <div class="w-1/2 h-12 p-12">
        <div  class="border-2">
          <accordion-wrapper
          v-for="(accordion, index) in accordions"
          :key="index"
          @accordion-wrapper-state-change="setAccordionWrapperState($event, index)"
          :on="accordion.active"
          :label="`${(index + 1)}. ${accordion.label}`"
          :body="accordion.body">
          </accordion-wrapper>
        </div>
      </div>
    </div>
        <div class="flex mb-4">
      <div class="w-1/2 h-12 p-12">
          <calendar-wrapper></calendar-wrapper>
      </div>
       <div class="w-1/2 h-12 p-12"></div>
      </div>
  </div>
</template>

<script>
import ToggleWrapper from './components/ToggleWrapper.vue'
import AccordionWrapper from './components/AccordionWrapper'
import CalendarWrapper from './components/CalendarWrapper'

// Main App component. Contains examples.
export default {
  name: 'App',
  components: {
    ToggleWrapper,
    AccordionWrapper,
    CalendarWrapper
  },
  data () {
    return {
      toggleWrapperState: false,
      accordions: [
        {
          label: 'This is an accordion',
          body: '<p>It is made up of multiple Toggle components</p>',
          active: true
        },
        {
          label: 'Loop over an array to populate it',
          body: '<p>Each array item needs a label, body and active state</p>',
          active: false
        },
        {
          label: 'Requires no additional methods',
          body: '<p>We get all this functionality from Toggle</p>',
          active: false
        },
        {
          label: 'But we can add methods if we like',
          body: '<p>For example, to emit additional state</p>',
          active: false
        },
        {
          label: 'Accessibility',
          body: '<p>In this example, each header is a button - so Tab and Space work! :D</p>',
          active: false
        }
      ]
    }
  },
  methods: {
    // @vuese
    // Receives emitted `toggle-wrapper-state-change` from `ToggleWrapper` component. Updates `toggleWrapperState`.
    setToggleWrapperState (toggleState) {
      this.toggleWrapperState = toggleState
    },
    // @vuese
    // Receives emitted `accordion-wrapper-state-change` from `AccordionWrapper` component. Updates active state of accordion.
    // In this example, we also close the other accordions.
    setAccordionWrapperState (accordionState, index) {
      this.accordions.forEach((x) => {
        // close all accordions.
        x.active = false
      })
      // update active state (could be true or false) of accordion we just clicked.
      this.accordions[index].active = accordionState
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
