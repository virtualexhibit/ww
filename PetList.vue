<template>
  <h6>{{ merged.display.name }}</h6>
  <button @click="toggleDetails()">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
  <ul v-if="detailsAreVisible">
    <li><strong>Age:</strong> {{ merged.display.age }}</li>
    <li><strong>Breed:</strong> {{ merged.display.breed }}</li>
    <li><strong>Gender:</strong> {{ merged.display.gender }}</li> 
    <li><strong>Type:</strong> {{ merged.display.petType }}</li> 
<li><strong>Vaccines:</strong> {{ merged.display.vaccines?.join(', ') || 'None' }}</li>

  </ul>
</template>
 
<script>
import { PetListRecipe } from '../recipes/rPetList.js'
export default {
  name: 'PetList',
  props: {
    item: { type: Object, default: () => ({}) },
  },
  data() {
    return {
      detailsAreVisible: false,
    }
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible
    },
  },
  computed: {
    merged() {
      return {
        ...PetListRecipe,
        ...this.item,
      }
    },
  },
}
</script>