<template>
  <div class="form-check my-2">
    <!-- label (optional) -->
    <label v-if="merged.display?.text">{{ merged.display.text }}</label>

    <!-- input with v-model support -->
    <input v-bind="merged.directives" v-model="inputValue"   />
  </div>
</template>

<script>
import { INPUT_RECIPE } from '../recipes/rTextBox.js'

export default {
  name: 'TextInput',
  props: {
    item: { type: Object, required: false, default: () => ({}) },
    modelValue: { type: String, default: "" }, 
    error: { type: String, default: "" }
  },
  computed: {
    merged() {
      return {
        directives: {
          ...INPUT_RECIPE.directives,
          ...this.item.directives,
        },
        display: {
          ...INPUT_RECIPE.display,
          ...this.item.display,
        },
      }
    },
    inputValue: { 
      get() {
        return this.modelValue
      },
      set(val) {
        this.$emit("update:modelValue", val)
      },
    },
  },
}
</script>
