<template>
  <div class="registration-form">
    <h2>Registration </h2>
    <form class="row" @submit.prevent="handleSubmit">
    
    <component
      v-for="(field, index) in REGISTRATION.inputs"
      :is="field.component"
      :key="index"
      :item="field"
      v-model="userInputs[field.key]"
    />


       <component
      v-for="(field, index) in REGISTRATION.buttons"
      :is="field.component"
      :key="index"
      :item="field"
      @click="handleAddClick(field)"
    />
  </form>

 

  </div>
</template>

<script>
import TextInput from "@/components/common/TextInput.vue"
import TextAreaInput from "@/components/common/TextAreaInput.vue"
import SelectInput from "@/components/common/SelectInput.vue"
import RadioInput from "@/components/common/RadioInput.vue"
import CheckBoxInput from "@/components/common/CheckBoxInput.vue"
import AddButton from "@/components/common/AddButton.vue"
import { REGISTRATION } from "../recipes/rRegistrationForm.js"

export default {
  name: "RegistrationForm",
  components: { 
    TextInput, 
    RadioInput, 
    CheckBoxInput, 
    AddButton, 
    TextAreaInput, 
    SelectInput 
  },
  data() {
    return {
      REGISTRATION,
      userInputs: {
        name: '',
        age: 0,
        breed: '',
        gender: '',
        petType: '',
        vaccines: [],
      }
    }
  },
  methods: {
    handleAddClick(field) {
      if (field.component === "AddButton") {
        this.handleSubmit()
      }
    },
    handleSubmit() {
      this.$emit('add-pet', { ...this.userInputs, id: new Date().toISOString() })
      this.userInputs = {
        display: {
          name: '',
          age: 0,
          breed: '',
          gender: '',
          petType: '',
          vaccines: [],

        },
      }
    },
    insertUserInputs(key, inputs) {
      console.log('a', key, inputs)
      this.userInputs[key] = inputs
      console.log(this.userInputs[key])
    },
  },
}
</script>


<style scoped>
.registration-form {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
}
</style>
