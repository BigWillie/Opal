# Toggle

Renderless component. Provides toggle functionality. Has one slot which you can use to inject your own markup. <br><br><u>Render</u></br>Returns `currentState`, `setOn`, `setOff`, `toggle`, `label` for use with v-slot. Use with your own html.

## Props

<!-- @vuese:Toggle:props:start -->
|Name|Description|Type|Required|Default|
|---|---|---|---|---|
|on|Sets initial state of toggle true or false (on/off).|`Boolean`|`false`|-|
|toggleLabel|String used for toggle's label.|`String`|`false`|-|

<!-- @vuese:Toggle:props:end -->


## Events

<!-- @vuese:Toggle:events:start -->
|Event Name|Description|Parameters|
|---|---|---|
|state-change|Emits state of current toggle state to parent. Required for parent to receive updated toggle state|-|

<!-- @vuese:Toggle:events:end -->


## Slots

<!-- @vuese:Toggle:slots:start -->
|Name|Description|Default Slot Content|
|---|---|---|
|default|-|-|

<!-- @vuese:Toggle:slots:end -->


## Methods

<!-- @vuese:Toggle:methods:start -->
|Method|Description|Parameters|
|---|---|---|
|setOn|Sets the toggle state to on (true).|-|
|setOff|Sets the toggle state to off (false).|-|
|toggle|Toggles the toggle state.|-|

<!-- @vuese:Toggle:methods:end -->


