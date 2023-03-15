<template>
  <form class="recipe-edit-form" @submit.prevent="saveChanges">
    <!-- Title  -->
    <input class="recipe-edit-title-input" type="text" v-model="mutableData.title">

    <!-- Description  -->
    <input class="recipe-edit-description-input" v-model="mutableData.description">

    <!-- Ingredients List -->
    <div class="recipe-ingredient" v-for="item,index of mutableData.ingredients" :key="index">
      <input class="recipe-ingredient-input" v-model="mutableData.ingredients[index]">
      <button class="recipe-ingredient-delete-button" type="button" @click="deleteIngredient(index)">X</button>
    </div>

    <!-- New ingredient field -->
    <div class="recipe-new-ingredient">
      <input class="recipe-new-ingredient-input" v-model="newIngredient">
      <button class="recipe-new-ingredient-add-button" type="button" :disabled="newIngredient === ''" placeholder="Add a new ingredient..." @click="addIngredient">Add</button>
    </div>

    <div class="recipe-edit-actions">
      <button class="recipe-edit-save-button" type="submit">Save</button>
      <button class="recipe-edit-cart-button" type="button" @click="addToList">Add to shopping list</button>
    </div>
  </form>
</template>

<script>
export default {
  name: 'RecipeDetail',
  props: {
    recipeIndex: Number,
    initialData: Object
  },
  emits: [
    'dataChanged',
    'addToList'
  ],
  mounted() {
    this.mutableData = {...this.initialData}
  },
  data() {
    return {
      mutableData:{
        title: "",
        description: "",
        ingredients: []
      },
      newIngredient: ""
    }
  },
  methods: {
    addIngredient(){
      this.mutableData.ingredients.push(this.newIngredient);
      this.newIngredient = ""
    },
    deleteIngredient(index){
      this.mutableData.ingredients.splice(index,1);
    },
    saveChanges(){
      this.$emit('dataChanged', this.recipeIndex, this.mutableData)
    },
    addToList(){
      this.$emit('addToList', this.recipeIndex)
    }
  }
}
</script>