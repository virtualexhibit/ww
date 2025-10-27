<template>
  <div class="text-center mt-3">
    <button
      v-for="(btn, index) in merged.buttons"
      :key="index"
      :class="btn.class"
      @click="$emit(btn.event)"
      :disabled="isDisabled(btn.event)"

    >
      {{ btn.text }}
    </button>
  </div>
</template>

<script>
import { BUTTONS_RECIPE } from '../Recipes/rButtons.js'

export default {
  name: 'SomeButtons',
  props: {
    item: { type: Object, default: () => ({}) },
    //     disableClearCompleted: { type: Boolean, default: true },
    // disableClearAll: { type: Boolean, default: true },

  },
  computed: {
    merged() {
      return {
        ...BUTTONS_RECIPE,
        ...this.item,
      }
    },
  },
  // methods:{isDisabled(event) {
  //     if (event === 'clear-completed') return this.disableClearCompleted
  //     if (event === 'clear-all') return this.disableClearAll
  //     return false
  //   },}
}
</script>


<!-- <style scoped>
button {
  margin: 0 5px;
}
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style> -->
