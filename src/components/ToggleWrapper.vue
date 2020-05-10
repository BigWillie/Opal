<template>
      <toggle @state-change="stateChange($event)" :on="on" :toggle-label="toggleLabel">
      <template v-slot="{toggle, currentState, label}">
        <div class="toggleComp">
            <label class="flex items-center cursor-pointer">
                <!-- toggle -->
                <div class="relative">
                    <!-- input -->
                    <div class="hidden-wrap">
                        <input :checked="currentState" type="checkbox" @change="toggle()" />
                    </div>
                    <!-- line -->
                    <div :class="{'toggle-line-on' : currentState}" class="toggle-line w-10 h-4 bg-gray-400 rounded-full shadow-inner"></div>
                    <!-- dot -->
                    <div :class="{'toggle-dot-on' : currentState}" class="toggle-dot absolute w-6 h-6 bg-white rounded-full shadow inset-y-0 left-0"></div>
                </div>
                <!-- label -->
                <div class="ml-3 text-gray-700 font-medium">{{label}}</div>
            </label>
        </div>
      </template>
    </toggle>
</template>

<script>

import Toggle from './Toggle'
/**
 * @group HTML WRAPPERS
 * <u>Component html wrapper for Toggle.</u><br>
 * Imports Toggle renderless component. Provides default html. Use this 'as-is' or as a starting point for your own markup.
 * <br><br><u>v-slot</u><br>Accepts the following from Toggle: `currentState`, `setOn`, `setOff`, `toggle`, `label`
 * <br><br><u>Accessibility</u><br>Native checkbox. <a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role">https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role</a>
 * <br>`TAB` to focus, `SPACE` to check/uncheck.
 */
export default {
  name: 'ToggleWrapper',
  components: {
    Toggle
  },
  props: {
    // Is the toggle 'on' or 'off' - passed to set initial state of renderless Toggle component.
    on: { type: Boolean, default: false },
    // String used for toggle's label - passed to renderless Toggle component.
    toggleLabel: String
  },
  methods: {
    stateChange ($event) {
    // Emits toggle state to parent (in this case, `toggle-wrapper-state-change`. Required for parent to receive updated toggle state.
      this.$emit('toggle-wrapper-state-change', $event)
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
