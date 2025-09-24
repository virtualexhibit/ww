<template>
  <div class="slamboo-container">
    <div class="text-center mb-3">
      <header><h4>SlamBoo</h4></header>
    </div>

    <!-- Navigation buttons -->
    <div class="d-grid gap-2 d-md-flex justify-content-md-center mb-4">
      <component
        v-for="(field, index) in slamBooRecipe.navButtons"
        :is="field.component"
        :key="index"
        :item="field"
        :class="[
          'btn',
          currentAction === field.on.action ? 'btn-success active' : 'btn-secondary'
        ]"
        @click="navButtonIsClick(field)"
      />
    </div>

    <!-- Registration form -->
    <RegistrationForm
      v-if="showRegistrationForm"
      @add-pet="addPet"
    />

    <!-- Pet list -->
    <div v-if="showPetList" class="list-container">
      <h5 class="text-center">Pet List</h5>

      <div v-if="slamBooRecipe.pets.length === 0" class="text-center text-muted">
        No pets added yet.
      </div>

      <component
        v-else
        v-for="(field, index) in slamBooRecipe.pets.filter(pet => pet.display?.name)"
        :is="field.component"
        :key="index"
        :item="field"
      />
    </div>
  </div>
</template>

<script>
import { PetFolioRecipe } from '../recipes/rPetFolio.js'
import AddButton from '../common/AddButton.vue'
import RegistrationForm from './RegistrationForm.vue'
import PetList from '../common/PetList.vue'

export default {
  name: 'SlamBoo',
  components: { AddButton, RegistrationForm, PetList },
  data() {
    return {
      slamBooRecipe: PetFolioRecipe,
      showRegistrationForm: false,
      showPetList: true,
      currentAction: 'petList' // Pet List is default active
    }
  },
  methods: {
    navButtonIsClick(field) {
      this.currentAction = field.on?.action

      if (field.on?.action === 'addPet') {
        this.showRegistrationForm = true
        this.showPetList = false
      }
      if (field.on?.action === 'petList') {
        this.showRegistrationForm = false
        this.showPetList = true
      }
    },
    addPet(pet) {
      this.slamBooRecipe.pets.unshift({
        component: "PetList",
        id: pet.id,
        display: { ...pet }
      })
      this.showRegistrationForm = false
      this.showPetList = true
      this.currentAction = 'petList'
    }
  }
}
</script>
