<template>
      <calendar @state-change="stateChange($event)" :on="currentState" :label="label">
      <template v-slot="{next, previous, jump, calendarGrid, pickDate}">
        <div class="calendarComp">
            {{next}}
            {{previous}}
            {{jump}}
            <table class="table-auto">
                <thead>
                    <tr>
                        <th>Sun</th>
                        <th>Mon</th>
                        <th>Tue</th>
                        <th>Wed</th>
                        <th>Thu</th>
                        <th>Fri</th>
                        <th>Sat</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(week, index) in calendarGrid" :key="index">
                        <td class="border px-4 py-2" :class="cellClass(day && day.day)" v-for="(day, index) in week" :key="index">
                            <button @click="pickDate(day.day)" v-if="day && day.day">
                                {{day.day}}
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
      </template>
    </calendar>
</template>

<script>

import Calendar from './Calendar'
/**
 * @group HTML WRAPPERS
 * <u>Component html wrapper for Toggle.</u><br>
 * Imports Toggle renderless component. Provides default html. Use this 'as-is' or as a starting point for your own markup.
 * <br><br><u>v-slot</u><br>Data is sent into the toggle component via Props. The Toggle component's render method returns the following `active`, `setOn`, `setOff`, `toggle`, `label`, `body` for use with your html.
 * <br><br><u>Accessibility</u><br>Native checkbox. <a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role">https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role</a>
 * <br>`TAB` to focus, `SPACE` to check/uncheck.
 */
export default {
  name: 'CalendarWrapper',
  components: {
    Calendar
  },
  props: {
    // Is the toggle 'on' or 'off. Passed into renderless Toggle component to set initial state.
    on: { type: Boolean, default: false },
    // String used for toggle's label. Passed into renderless Toggle component to set toggle label.
    label: String
  },
  methods: {
    stateChange ($event) {
    // Emits toggle state to parent (in this case, `toggle-wrapper-state-change`. Required for parent to receive updated toggle state.
      this.$emit('toggle-wrapper-state-change', $event)
    },
    cellClass (day) {
      return day ? '' : 'bg-gray-100'
    }
  },
  computed: {
    // Received prop as a computed property, forcing the component to update
    currentState () {
      return this.on
    }
  }
}
</script>

<style>

</style>
