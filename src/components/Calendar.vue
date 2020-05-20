<script>
export default {
  name: 'Calendar',
  props: {
    yearIndex: {
      type: Number
    },
    monthIndex: {
      type: Number
    },
    months: {
      type: Array,
      default () {
        return ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
      }
    }
  },
  mounted () {
    if (!this.selectedYear) {
      this.selectedYear = this.currentYear
    }
    if (!this.selectedMonth) {
      this.selectedMonth = this.currentMonth
    }
    this.updateCalendar()
  },
  data () {
    return {
      today: new Date(),
      selectedYear: this.yearIndex,
      selectedMonth: this.monthIndex,
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
    jump () {
      this.updateCalendar(this.selectedMonth, this.selectedMonth)
    },
    updateCalendar (month = this.selectedMonth, year = this.selectedYear) {
      const getDateFunc = (day) => {
        return day.getDate()
      }
      const getDayFunc = (day) => {
        return day.getDay()
      }
      const getFullYearFunc = (day) => {
        return day.getFullYear()
      }
      const getMonthFunc = (day) => {
        return day.getMonth()
      }
      const isTodayFunc = (day) => {
        return (day === getDateFunc(this.today) && year === getFullYearFunc(this.today) && month === getMonthFunc(this.today))
      }

      // clearing all previous dates
      const totalDays = this.daysInMonth
      this.dates = ([...Array(totalDays).keys()].map(x => ++x)).map((day) => {
        const p = new Date(year, month, day)
        return {
          day: day,
          isToday: isTodayFunc(day),
          weekday: getDayFunc(p),
          month: month,
          year: year,
          dateObj: p
        }
      })
    }
  },
  computed: {
    calendarGrid () {
      // const days = this.daysInMonth
      // const gridSize = Math.ceil(days / 7)
      const chunks = [[]]
      const rowChunk = (x) => {
        const [head, ...tail] = x

        if (head && head.weekday < 6) {
          chunks[chunks.length - 1].push(head)
          rowChunk(tail)
        } else if (head && head.weekday === 6) {
          // new week
          chunks[chunks.length - 1].push(head)
          chunks.push([]) // create empty array on chunk
          rowChunk(tail)
        }
      }
      rowChunk(this.dates)
      const padStartCount = 7 - chunks[0].length
      const padEndCount = 7 - chunks[chunks.length - 1].length
      const padStartArr = [...Array(padStartCount).keys()].map(x => {})
      const padEndArr = [...Array(padEndCount).keys()].map(x => {})

      chunks[0] = padStartArr.concat(chunks[0])
      chunks[chunks.length - 1] = chunks[chunks.length - 1].concat(padEndArr)
      return chunks
    },
    daysInMonth () {
      return 32 - new Date(this.selectedYear, this.selectedMonth, 32).getDate()
    },
    currentMonth () {
      return this.today.getMonth()
    },
    currentYear () {
      return this.today.getFullYear()
    }
  },
  render () {
    // Data / methods that you'd like to make available to the slot
    return this.$scopedSlots.default({
      next: this.next,
      previous: this.previous,
      jump: this.jump,
      calendarGrid: this.calendarGrid,
      pickDate: this.pickDate
    })
  }
}
</script>
