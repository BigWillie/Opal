# ToggleWrapper

<u>Component html wrapper for Toggle.</u><br> Imports Toggle renderless component. Provides default html. Use this 'as-is' or as a starting point for your own markup. <br><br><u>v-slot</u><br>Data is sent into the toggle component via Props. The Toggle component's render method returns the following `active`, `setOn`, `setOff`, `toggle`, `label`, `body` for use with your html. <br><br><u>Accessibility</u><br>Native checkbox. <a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role">https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/checkbox_role</a> <br>`TAB` to focus, `SPACE` to check/uncheck.

## Props

<!-- @vuese:ToggleWrapper:props:start -->
|Name|Description|Type|Required|Default|
|---|---|---|---|---|
|on|Is the toggle 'on' or 'off. Passed into renderless Toggle component to set initial state.|`Boolean`|`false`|-|
|label|String used for toggle's label. Passed into renderless Toggle component to set toggle label.|`String`|`false`|-|

<!-- @vuese:ToggleWrapper:props:end -->


## Events

<!-- @vuese:ToggleWrapper:events:start -->
|Event Name|Description|Parameters|
|---|---|---|
|toggle-wrapper-state-change|Emits toggle state to parent (in this case, `toggle-wrapper-state-change`. Required for parent to receive updated toggle state.|-|

<!-- @vuese:ToggleWrapper:events:end -->


