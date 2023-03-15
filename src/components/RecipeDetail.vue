<template>
  <form @submit.prevent="saveChanges">
    <!-- Title  -->
    <input type="text" v-model="mutableData.title">
    <br>

    <!-- Description  -->
    <textarea v-model="mutableData.description"
      rows="10" cols="40"
    >
    </textarea>
    <br>

    <!-- Ingredients List -->
    <template v-for="item,index of mutableData.ingredients" :key="index">
      <input v-model="mutableData.ingredients[index]">
      <br>
    </template>

    <!-- New ingredient field -->
    <input v-model="newIngredient">
    <button type="button" @click="addIngredient">Add</button>
    <br>

    <button type="submit">Save</button>
    <button type="button" @click="addToList">Add to shopping list</button>
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
    saveChanges(){
      this.$emit('dataChanged', this.recipeIndex, this.mutableData)
    },
    addToList(){
      this.$emit('addToList', this.recipeIndex)
    }
  }
}
</script>