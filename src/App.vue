
<template>
  <h1>Recipe Book</h1>
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
      selectedRecipe: null
    }
  }
  
}
</script>


<style scoped>
</style>
