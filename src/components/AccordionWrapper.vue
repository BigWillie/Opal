<template>
      <toggle @state-change="stateChange($event)" :on="currentState" :label="label" :body="body">
      <template v-slot="{toggle, active, label, body}">
        <div class="accordionComp">
                <div class="accordion-header p-1">
                    <button type="button"
                    class="w-full flex justify-between bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 focus:bg-blue-600 focus:outline-none focus:shadow-outline"
                    @click="toggle()">
                        <span>{{label}}</span>
                        <font-awesome-icon v-show="active" :icon="['fas' , 'angle-down']"></font-awesome-icon>
                        <font-awesome-icon v-show="!active" :icon="['fas' , 'angle-up']"></font-awesome-icon>
                    </button>
                </div>
                <div class="p-2 text-left" v-show="active" v-html="body"></div>
        </div>
      </template>
    </toggle>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
// import { name of your icon in camelCase } from "@fortawesome/free-solid-svg-icons";
// For example, I want to use fa-enveloper-open-text, then it's faEnvelopeOpenText
import { faAngleDown, faAngleUp } from '@fortawesome/free-solid-svg-icons'

import Toggle from './Toggle'

// Then add it to library
library.add([faAngleUp, faAngleDown])

/**
 * @group HTML WRAPPERS
 * <u>Component html wrapper for Toggle.</u><br>
 * Imports Toggle renderless component. Provides default html. Use this 'as-is' or as a starting point for your own markup.
 * <br><br><u>v-slot</u><br>Data is sent into the toggle component via Props. The Toggle component's render method returns the following `currentState`, `setOn`, `setOff`, `toggle`, `label` for use with your html.
 * <br><br><u>Accessibility</u><br>Native checkbox. <a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role">https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role</a>
 * <br>`TAB` to focus, `SPACE` to check/uncheck.
 */
export default {
  name: 'AccordionWrapper',
  components: {
    Toggle
  },
  props: {
    // Is the toggle 'on' or 'off. Passed into renderless Toggle component to set initial state.
    on: { type: Boolean, default: false },
    // String used for toggle's label. Passed into renderless Toggle component to set toggle label.
    label: String,
    body: String
  },
  methods: {
    stateChange ($event) {
      // Emits toggle state to parent (in this case, `toggle-wrapper-state-change`. Required for parent to receive updated toggle state.
      this.$emit('accordion-wrapper-state-change', $event)
    }
  },
  computed: {
    currentState () {
      return this.on
    }
  }
}
</script>

<style>
.toggleComp .hidden-wrap {
    height: 1px;
    width: 1px;
    overflow: hidden;
}
.toggleComp .toggle-dot {
    top: -.25rem;
    left: -.25rem;
    transition: all 0.3s ease-in-out;
}
/* Adds focus styles to .toggle-dot when checkbox has focus */
.toggleComp:focus-within .toggle-dot {
    box-shadow: 0 0 0 3px rgba(66, 153, 225, 0.5);
}
.toggleComp .toggle-dot-on {
    transform: translateX(100%);
    background-color: #48bb78;
}
</style>
