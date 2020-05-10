# ToggleWrapper

<u>Component html wrapper for Toggle.</u><br> Imports Toggle renderless component. Provides default html. Use this 'as-is' or as a starting point for your own markup. <br><br><u>v-slot</u><br>Accepts the following from Toggle: `currentState`, `setOn`, `setOff`, `toggle`, `label` <br><br><u>Accessibility</u><br>Native checkbox. <a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role">https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role</a> <br>`TAB` to focus, `SPACE` to check/uncheck.

## Props

<!-- @vuese:ToggleWrapper:props:start -->
|Name|Description|Type|Required|Default|
|---|---|---|---|---|
|on|Is the toggle 'on' or 'off' - passed to set initial state of renderless Toggle component.|`Boolean`|`false`|-|
|toggleLabel|String used for toggle's label - passed to renderless Toggle component.|`String`|`false`|-|

<!-- @vuese:ToggleWrapper:props:end -->


## Events

<!-- @vuese:ToggleWrapper:events:start -->
|Event Name|Description|Parameters|
|---|---|---|
|toggle-wrapper-state-change|Emits toggle state to parent (in this case, `toggle-wrapper-state-change`. Required for parent to receive updated toggle state.|-|

<!-- @vuese:ToggleWrapper:events:end -->


