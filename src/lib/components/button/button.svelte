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

<button
  {disabled}
  aria-disabled={disabled}
  {name}
  {type}
  {value}
  {formtarget}
  class="svb-{style} svb-hover-{hover} svb-focus-{focus} {color}"
>
  <slot />
</button>

<style lang="scss">
  @import "../../style/mainVar.scss";
  @import "./buttonVar.scss";

  button {
    cursor: pointer;

    font-family: var(--font, $font);
    font-size: var(--font-size, $font-size);

    padding: var(--vertical-button-padding, $vertical-button-padding) var(--horizontal-button-padding, $horizontal-button-padding);

    border-radius: var(--button-radius, $button-radius);

    transition: all var(--hover-transition-duration, $hover-transition-duration);

    color: #ffffff;
    border: none;
    outline: none;

    // All possible color variants
    &.primary {
      background-color: var(--primary, $primary);
      border-color: var(--primary, $primary);

      &.svb-stroked {
        color: var(--primary, $primary);
      }
    }
    &.warn {
      background-color: var(--warn, $warn);
      border-color: var(--warn, $warn);

      &.svb-stroked {
        color: var(--warn, $warn);
      }
    }
    &.caution {
      background-color: var(--caution, $caution);
      border-color: var(--caution, $caution);

      &.svb-stroked {
        color: var(--caution, $caution);
      }
    }
    &.basic {
      background-color: var(--fill-color, $fill-color);
      color: var(--color, $color);

      border: solid 1px var(--border-color, $border-color);

      &.svb-stroked {
        color: var(--primary, $primary);
      }
    }

    // All button styles
    &.svb-raised {
      box-shadow: 2px 2px 3px var(--border-color, $border-color);
    }
    &.svb-link {
      background: none;
      border: none;
      color: var(--color, $color);
    }
    &.svb-round {
      padding: var(--rounded-button-padding, $rounded-button-padding);
      border-radius: 50%;
      width: 75px;
      height: 75px;
    }
    &.svb-round-s {
      padding: var(--rounded-button-padding, $rounded-button-padding);
      border-radius: 50%;
      height: 50px;
      width: 50px;
    }
    &.svb-round-xs {
      padding: var(--xs-rounded-button-padding, $xs-rounded-button-padding);
      border-radius: 50%;
      height: 30px;
      width: 30px;
    }
    &.svb-stroked {
      background: none;
      border: solid 1px;
    }

    // Button style on hover
    &:hover.svb-hover-invert {
      background: var(--fill-color, $fill-color);

      &.primary {
        color: var(--primary, $primary);
      }
      &.warn {
        color: var(--warn, $warn);
      }
      &.caution {
        color: var(--caution, $caution);
      }
      &.basic {
        background: var(--color, $color);
        color: var(--basic, $basic);
      }
    }

    // All styles for button hover
    &:hover.svb-hover-brighten {
      filter: brightness(115%);
    }
    &:hover.svb-hover-darken {
      filter: brightness(85%);
    }
    &:hover.svb-hover-grow {
      transform: scale(1.05);
    }
    &:hover.svb-hover-raise {
      box-shadow: 3px 3px 3px var(--border-color, $border-color);
    }
    &:hover.svb-hover-reduce {
      box-shadow: 0 0 0;
    }

    // All styles for button active
    //changing active transition time
    &:active {
      transition-duration: var(--click-transition-duration, $click-transition-duration);
    }
    &:active.svb-focus-brighten {
      filter: brightness(115%);
    }
    &:active.svb-focus-darken {
      filter: brightness(85%);
    }
    &:active.svb-focus-grow {
      transform: scale(1.05);
    }
    &:active.svb-focus-raise {
      box-shadow: 3px 3px 3px var(--border-color, $border-color);
    }
    &:active.svb-focus-reduce {
      box-shadow: 0 0 0;
    }
  }
</style>
