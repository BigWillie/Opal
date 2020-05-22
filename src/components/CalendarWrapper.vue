<template>
      <calendar @update-month-year="onMonthYearSelected" :startYearProp="year" :startMonthProp="month">
      <template v-slot="{next, previous, jump, calendarGrid, pickDate, monthLabels, yearLabels}">
        <div class="calendarComp">
            <div class="flex mb-4">
                <div class="w-1/4 pr-2">
                    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="previous()">
                        <font-awesome-icon :icon="['fas' , 'caret-left']"></font-awesome-icon>
                    </button>
                </div>
                <div class="w-1/4 pr-2">
                    <select @change="jump(month, year)" v-model="month" class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500">
                        <option v-for="(month, index) in monthLabels" :key="month" :value="index">{{month}}</option>
                    </select>
                </div>
                <div class="w-1/4 pl-2">
                        <select @change="jump(month, year)" v-model="year" class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500">
                            <option v-for="year in yearLabels" :key="year" :value="year">{{year}}</option>
                        </select>
                </div>
                <div class="w-1/4 pr-2">
                    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="next()">
                        <font-awesome-icon :icon="['fas' , 'caret-right']"></font-awesome-icon>
                    </button>
                </div>
            </div>
            <table class="table-auto w-full">
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
                            <button @click="pickDate(day.day)" v-if="day && day.day" :title="day.dateString">
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
import { library } from '@fortawesome/fontawesome-svg-core'
// import { name of your icon in camelCase } from "@fortawesome/free-solid-svg-icons";
// For example, I want to use fa-enveloper-open-text, then it's faEnvelopeOpenText
import { faCaretLeft, faCaretRight } from '@fortawesome/free-solid-svg-icons'

import Calendar from './Calendar'

// Then add it to library
library.add([faCaretLeft, faCaretRight])
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
  mounted () {
    // for demo puporses - sets our initial year / month
    const today = new Date()
    this.year = today.getFullYear()
    this.month = today.getMonth()
  },
  data () {
    return {
      year: null,
      month: null
    }
  },
  methods: {
    onMonthYearSelected ($event) {
    // Emits toggle state to parent (in this case, `toggle-wrapper-state-change`. Required for parent to receive updated toggle state.
      this.year = $event.year
      this.month = $event.month
    },
    cellClass (day) {
      return day ? '' : 'bg-gray-100'
    }
  }
}
</script>

<style>

</style>
