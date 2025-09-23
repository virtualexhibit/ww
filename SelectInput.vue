<template>
  <div class="mb-3">
    <label class="input-label">{{ item.display.text }}</label>
    <select
      class="form-select"
      v-bind="item.directives"
      v-model="inputValue"
    >
      <option
        v-for="(option, idx) in item.options"
        :key="idx"
        :value="option.value"
      >
        {{ option.text }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "SelectInput",
  props: {
    item: { type: Object, required: true },
    modelValue: { type: String, default: "" }
  },
  computed: {
    inputValue: {
      get() {
        return this.modelValue
      },
      set(val) {
        this.$emit("update:modelValue", val)
      }
    }
  }
}
</script>



<!-- in the recipe -->
<!-- {
  component: "SelectInput",
  directives: { name: "pet_type", class: "form-select" },
  display: { text: "Pet Type:" },
  options: [
    { value: "dog", text: "Dog" },
    { value: "cat", text: "Cat" },
    { value: "other", text: "Other" }
  ]
}, -->