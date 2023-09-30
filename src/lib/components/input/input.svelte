<script lang="ts">
    import type { Colors } from "$lib/types.js";
  import type { InputVariant, InputmodeVariant } from "./types.js";

  /** Input's name */
  export let name: string;
  /** Input's color */
  export let color: Colors = "primary";
  /** Shown label */
  export let label: string = "Name";
  /** If the input has a background or not */
  export let fill: boolean = false;
  /** Remove the label to just keep the input */
  export let simple: boolean = false;
  /** Input's type */
  export let type: InputVariant = "text";
  /** Input's placeholder */
  export let placeholder: string | null = null;
  /** Input's width */
  export let width: string = "20%";
  /** If input's required */
  export let required: boolean = false;
  /** Input's minimum length */
  export let minlength: number = 0;
  /** Input's maximum length */
  export let maxlength: number = 100;
  /** Input's pattern */
  export let pattern: string | null = null;
  /** Show keyboard when focusing on the input */
  export let inputmode: InputmodeVariant = null;
  /** If the input's readonly */
  export let readonly: boolean = false;
  /** If the input's disabled */
  export let disabled: boolean = false;

  /** Define if the label is reduced */
  let reduceLabel: boolean = false;

  /**
   * Check if the input has content in it or is focused to reduce label
   *
   * @param {event} Event Event
   */
  const handleInputLength = (event: Event) => {
    const input = event.target as HTMLInputElement;

    input.value.length > 0 || input === document.activeElement ? (reduceLabel = true) : (reduceLabel = false);
  };
</script>

{#if simple}
  <div class="svb-input-container" style="width: {width}">
    <input
      class="svb-input svb-simple {color}"
      id={name}
      {name}
      {type}
      {placeholder}
      aria-placeholder={placeholder}
      class:svb-fill={fill}
      class:svb-filled={reduceLabel}
      class:color={color}
      {required}
      aria-required={required}
      {minlength}
      {maxlength}
      {pattern}
      {inputmode}
      {readonly}
      aria-readonly={readonly}
      {disabled}
      aria-disabled={disabled}
      on:input={handleInputLength}
      on:click={() => {reduceLabel = true }}
      on:blur={handleInputLength}
    />
  </div>
{:else}
  <div class="svb-input-container" style="width: {width}">
    <input
      class="svb-input svb-complex {color}"
      id={name}
      {name}
      {type}
      {placeholder}
      aria-placeholder={placeholder}
      class:svb-fill={fill}
      class:svb-filled={reduceLabel}
      {required}
      aria-required={required}
      {minlength}
      {maxlength}
      {pattern}
      {inputmode}
      {readonly}
      aria-readonly={readonly}
      {disabled}
      aria-disabled={disabled}
      on:input={handleInputLength}
      on:click={() => {reduceLabel = true }}
      on:blur={handleInputLength}
    />
    <label for={name}>{label}</label>
  </div>
{/if}

<style lang="scss">
  @import "../../style/mainVar.scss";
  @import "./inputVar.scss";

  .svb-input-container {
    position: relative;

    &::after {
      content: "\A0";
      position: absolute;

      bottom: 0;
      left: 0;
      width: 100%;
      height: 3px;

      transition: transform 0.25s;
      transform-origin: left;
      transform: scaleX(0);

      background-color: #111111;
    }

    &:has(> .svb-input.primary)::after {
      background-color: var(--primary, $primary);
    }
    &:has(> .svb-input.caution)::after {
      background-color: var(--caution, $caution);
    }
    &:has(> .svb-input.warn)::after {
      background-color: var(--warn, $warn);
    }

    &:has(> .svb-input:focus)::after {
      transform: scaleX(1);
    }

    label {
      position: absolute;

      font-family: var(--font, $font);
      font-size: vazr(--font-size, $font-size);

      left: var(--left-input-padding, $left-input-padding);
      bottom: var(--bottom-input-padding, $bottom-input-padding);

      transition: all 0.15s;
    }

    .svb-input {
      border: none;
      outline: none;

      font-size: var(--font-size, $font-size);
      font-family: va(--font, $font);

      height: 100%;
      width: calc(100% - var(--right-input-padding, $right-input-padding) * 2);

      color: var(--color, $color);

      border-bottom: 2px var(--border-color, $border-color) solid;

      padding: var(--top-input-padding, calc($top-input-padding)) var(--right-input-padding, $right-input-padding)
        var(--bottom-input-padding, calc($bottom-input-padding / 2)) var(--left-input-padding, $left-input-padding);

      &.svb-fill {
        background-color: var(--fill-color, $fill-color);
      }

      &.svb-complex {
        &:not(:focus)::placeholder {
          color: transparent;
        }
      }

      &.svb-filled ~ label {
        bottom: 60%;

        font-size: 10px;

        color: #111111;
      }
      &:focus.primary ~ label {
        color: var(--primary, $primary);
      }
      &:focus.caution ~ label {
        color: var(--caution, $caution);
      }
      &:focus.warn ~ label {
        color: var(--warn, $warn);
      }
    }
  }
</style>