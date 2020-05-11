<script>
/*
* @group RENDERLESS
* Renderless component. Provides toggle functionality. Has one slot which you can use to inject your own markup.
* <br><br><u>Render</u></br>Returns `currentState`, `setOn`, `setOff`, `toggle`, `label` for use with v-slot. Use with your own html.
*/
export default {
  name: 'Toggle',
  props: {
    // Sets initial state of toggle true or false (on/off).
    on: { type: Boolean, default: false },
    // String used for toggle's label.
    toggleLabel: String
  },
  data () {
    return {
      currentState: this.on
    }
  },
  methods: {
    // @vuese
    // Sets the toggle state to on (true).
    setOn () {
      this.currentState = true
      // Emits state of current toggle state to parent. Required for parent to receive updated toggle state
      this.$emit('state-change', this.currentState)
    },
    // @vuese
    // Sets the toggle state to off (false).
    setOff () {
      this.currentState = false
      this.$emit('state-change', this.currentState)
    },
    // @vuese
    // Toggles the toggle state.
    toggle () {
      this.currentState = !this.currentState
      this.$emit('state-change', this.currentState)
    }
  },
  render () {
    // Data / methods that you'd like to make available to the slot
    return this.$scopedSlots.default({
      currentState: this.currentState,
      setOn: this.setOn,
      setOff: this.setOff,
      toggle: this.toggle,
      label: this.toggleLabel
    })
  }
}
</script>
