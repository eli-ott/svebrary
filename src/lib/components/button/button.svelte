<script lang="ts">
    import type { Colors } from "$lib/types.js";
  import type { ButtonVariant, HoverVariant, FocusVariant, TypeVariant, FormtargetVariant } from "./types.ts";

  /** Button type */
  export let type: TypeVariant = null;
  /** Button"s name */
  export let name: string;
  /** Button value */
  export let value: string | null = null;
  /** Button's form target */
  export let formtarget: FormtargetVariant = null;
  /** If the button is disabled */
  export let disabled: boolean = false;
  /** Button style */
  export let style: ButtonVariant = "raised";
  /** Button hover style */
  export let hover: HoverVariant = "invert";
  /** Button focus style */
  export let focus: FocusVariant = "brighten";
  /** Button's color */
  export let color: Colors = "primary";
</script>

<button {disabled} aria-disabled={disabled} {name} {type} {value} {formtarget} class="svb-{style} svb-hover-{hover} svb-focus-{focus} {color}">
  <slot />
</button>

<style lang="scss">
  @import "../../style/mainVar.scss";
  @import "./buttonVar.scss";

  button {
    font-family: var(--font, $font);
    font-size: var(--font-size, $font-size);

    padding: var(--vertical-button-padding, $vertical-button-padding) var(--horizontal-button-padding, $horizontal-button-padding);

    border-radius: var(--button-radius, $button-radius);

    color: #ffffff;
    border: solid 1px var(--border-color, $border-color);

    &.primary {
      background-color: var(--primary, $primary);
    }
    &.warn {
      background-color: var(--warn, $warn);
    }
    &.caution {
      background-color: var(--caution, $caution);
    }
    &.basic {
      background-color: var(--fill-color, $fill-color);
      color: var(--color, $color);
    }
  }
</style>
