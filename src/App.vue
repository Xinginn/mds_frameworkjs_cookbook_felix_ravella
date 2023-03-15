
<template>
  <h1>Recipe Book</h1>
  <form @submit.prevent="addRecipe">
    <input type="text" placeholder="Add a new recipe..." v-model="newRecipeTitle">
    <button type="submit">Add</button>
  </form>

  <RecipeButton v-for="item,index of recipes" 
    :key="index"
    :recipeIndex="index"
    :title="item.title"
    @requestEdit="(recipeIndex) => selectedRecipe = recipeIndex"
    @requestDelete="(recipeIndex) => recipes.splice(recipeIndex, 1)"
    />
</template>

<script lang="ts">
import RecipeButton from './components/RecipeButton.vue'

export default {
  name: 'App',
  components:{
    RecipeButton
  },
  data(){
    return {
      recipes: [
        {
          title: "Beef stew",
          description: "A delicious dish from England made with beef",
          ingredients: [
            "1 carrot",
            "2 potatoes",
            "200g beef"
          ]
        },        
        {
          title: "Cabage soup",
          description: "A delicious dish from England made with beef",
          ingredients: [
            "1 cabage",
            "3 potatoes",
            "2 onions"
          ]
        },
      ],
      selectedRecipe: null,
      newRecipeTitle: ""
    }
  },
  methods:{
    addRecipe(){
      this.recipes.push({
        title: this.newRecipeTitle,
        description: "",
        ingredients: []
      });
      this.newRecipeTitle = "";
    }
  }
  
}
</script>


<style scoped>
</style>
