<script>

function * dateGenerator ({ startDate = new Date(), increment = true, daycount = 1 }) {
  const day = startDate
  while (true) {
    yield {
      day: day.getDate(),
      weekday: day.getDay(),
      month: day.getMonth(),
      year: day.getFullYear(),
      dateString: day.toString()
    }
    if (increment) {
      day.setDate(day.getDate() + daycount)
    } else {
      day.setDate(day.getDate() - daycount)
    }
  }
}

function * monthLabelGenerator (start = new Date(2000, 0)) {
  const monthLabel = start
  while (true) {
    // should default to the locale date format
    yield monthLabel.toLocaleString({}, { month: 'short' })
    monthLabel.setMonth(monthLabel.getMonth() + 1)
  }
}

export default {
  name: 'Calendar',
  props: {
    yearProp: {
      type: Number
    },
    monthProp: {
      type: Number
    },
    monthLabelsProp: {
      type: Array
    },
    yearFromProp: {
      type: Number,
      default: 1979
    },
    yearCountProp: {
      type: Number,
      default: 150
    }
  },
  mounted () {
    if (!this.selectedYear) {
      this.selectedYear = this.currentYear
    }
    if (!this.selectedMonth) {
      this.selectedMonth = this.currentMonth
    }
    if (!this.months) {
      this.months = []
      const monthLabels = monthLabelGenerator()
      for (let i = 0; i < 12; i++) {
        const m = monthLabels.next().value
        this.months.push(m)
      }
    }
    this.updateCalendar()
  },
  data () {
    return {
      today: new Date(),
      selectedYear: this.yearProp,
      selectedMonth: this.monthProp,
      months: this.monthLabelsProp,
      dates: []
    }
  },
  methods: {
    pickDate (day) {
      alert(day)
    },
    next () {
      this.selectedYear = (this.selectedMonth === 11) ? this.selectedYear + 1 : this.selectedYear
      this.selectedMonth = (this.selectedMonth + 1) % 12
      this.updateCalendar(this.selectedMonth, this.selectedYear)
    },
    previous () {
      this.selectedYear = (this.selectedMonth === 0) ? this.selectedYear - 1 : this.selectedYear
      this.selectedMonth = (this.selectedMonth === 0) ? 11 : this.selectedMonth - 1
      this.updateCalendar(this.selectedMonth, this.selectedYear)
    },
    jump (month, year) {
      this.selectedMonth = month
      this.selectedYear = year
      this.updateCalendar(this.selectedMonth, this.selectedYear)
    },
    updateCalendar (month, year) {
      const xYear = year || this.selectedYear
      const xMonth = month || this.selectedMonth

      const totalDaysInMonth = 32 - new Date(xYear, xMonth, 32).getDate()

      const startDate = new Date(xYear, xMonth)

      const dates = dateGenerator({ startDate })

      const daysInMonth = []

      for (let i = 0; i < totalDaysInMonth; i++) {
        const d = dates.next().value
        daysInMonth.push(d)
      }

      this.dates = daysInMonth // updates with days in month
    }
  },
  computed: {
    years () {
      // Builds array of years
      const years = []
      const yearFrom = this.yearFromProp
      const yearCount = this.yearFromProp + this.yearCountProp
      for (let i = yearFrom; i <= yearCount; i++) {
        years.push(i)
      }
      return years
    },
    chunkWeeks () {
      // Splits days out into week long chunks
      // todo - add ability to change the day on which the week starts. Eg - monday.
      const chunks = [[]]
      const days = this.dates

      for (const day of days) {
        if (day.weekday === 6) {
          chunks[chunks.length - 1].push(day)
          chunks.push([]) // create a new week
        } else {
          chunks[chunks.length - 1].push(day)
        }
      }

      /*
      const padWeek = ({ week = [], increment, daycount = 1 }) => {
        // get first day in week
        const day = week[0]
        const startDate = new Date(day.dateString)

        if (!increment) {
          startDate.setDate(startDate.getDate() - daycount)
        } else {
          startDate.setDate(startDate.getDate() + daycount)
        }
        const dates = dateGenerator({ startDate, increment })
        const numberOfDays = increment ? (6 - day.weekday) : day.weekday

        console.log('to pad', numberOfDays)

        for (let i = 0; i < numberOfDays; i++) {
          const d = dates.next().value
          if (!increment) {
            week.unshift(d) // adds dates to START of week
          } else {
            week.push(d) // adds dates to END of week
          }
        }
        return week
      }

      if (chunks.length > 1) {
      // mutates the Chunk. Not the functional way, but its ok
      //  padWeek({ week: chunks[0], increment: false, daycount: 1 }) // pads first week
        padWeek({ week: chunks[chunks.length - 1], increment: true, daycount: 1 }) // pads end week
      }
      */

      const padStartCount = 7 - chunks[0].length
      const padEndCount = 7 - chunks[chunks.length - 1].length
      const padStartArr = [...Array(padStartCount).keys()].map(x => {})
      const padEndArr = [...Array(padEndCount).keys()].map(x => {})

      chunks[0] = padStartArr.concat(chunks[0])

      // Check we have an end chunk, and that chunk has at least 1 day in it.
      if (chunks.length > 1 && chunks[chunks.length - 1].length > 0) {
        chunks[chunks.length - 1] = chunks[chunks.length - 1].concat(padEndArr)
      }

      return chunks
    },
    currentMonth () {
      // used for supplying default selected in mount if no month provided
      return this.today.getMonth()
    },
    currentYear () {
      // used for supplying default selected in mount if no year provided
      return this.today.getFullYear()
    }
  },
  render () {
    // Data / methods that you'd like to make available to the slot
    return this.$scopedSlots.default({
      next: this.next,
      previous: this.previous,
      jump: this.jump,
      calendarGrid: this.chunkWeeks,
      monthLabels: this.months,
      yearLabels: this.years,
      pickDate: this.pickDate
    })
  }
}
</script>
