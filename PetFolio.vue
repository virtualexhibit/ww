<template>
  <div class="slamboo-container">
    <div class="text-center">
      <header><h4>SlamBoo</h4></header>
    </div>
 
    <form class="grid grid-cols-4 text-center">
      <component
        v-for="(field, index) in slamBooRecipe.navButtons"
        :is="field.component"
        :key="index"
        :item="field"
        @click="navButtonIsClick(field)"
      />
    </form>
 
    <RegistrationForm
      v-if="showRegistrationForm"
      @add-pet="addPet"
    />

   <div v-if="showPetList" class="list-container">
      <h5 class="text-center">Pet List</h5>
      <component
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
      showPetList: false,
    }
  },
  methods: {
    navButtonIsClick(field) {
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
        display: {
          name: pet.name,
          breed: pet.breed,
          age: pet.age,
          gender: pet.gender,
          petType: pet.petType,
          vaccines: pet.vaccines,
       
        }
      })
      this.showRegistrationForm = false
      this.showPetList = true
    }
  }
}
</script>


<style scoped>
.petfolio-form {
  max-width: 900px;       
  width: 100%;               
  margin: 40px auto;     
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background: #fff;        
  box-shadow: 0 2px 8px rgba(0,0,0,0.1); 
  box-sizing: border-box;
}

.petfolio-form h2 {
  text-align: center;
  margin-bottom: 20px;
}


</style>
