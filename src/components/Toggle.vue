<script>
/*
* @group RENDERLESS
* Renderless component. Provides toggle functionality. Has one slot which you can use to inject your own markup.
* <br><br><u>Render</u></br>Returns `active`, `setOn`, `setOff`, `toggle`, `label` for use with v-slot. Use with your own html.
*/
export default {
  name: 'Toggle',
  props: {
    // Sets initial state of toggle true or false (on/off).
    on: { type: Boolean, default: false },
    // String used for toggle's label.
    label: String,
    // For any arbitary body text (eg - if using Toggle to build an accordion)
    body: String
  },
  watch: {
    // watch for `On` prop updates. Update state when `On` changes.
    on (x) {
      this.currentState = x
    }
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
      // Explicitly set to demonstrate that state is $emitted up, and returned through the `on` prop
      this.currentState = true
      this.emitCurrentState()
    },
    // @vuese
    // Sets the toggle state to off (false).
    setOff () {
      this.currentState = false
      this.emitCurrentState()
    },
    // @vuese
    // Toggles the toggle state.
    toggle () {
      this.currentState = !this.currentState
      this.emitCurrentState()
    },
    // @vuese
    // Private method - not exposed over the scoped slot. Fires the emit.
    emitCurrentState () {
      // Emits state of current toggle state to parent. Required for parent to receive updated toggle state
      this.$emit('state-change', this.currentState)
    }
  },
  render () {
    // Data / methods that you'd like to make available to the slot
    return this.$scopedSlots.default({
      active: this.currentState,
      setOn: this.setOn,
      setOff: this.setOff,
      toggle: this.toggle,
      label: this.label,
      body: this.body
    })
  }
}
</script>
