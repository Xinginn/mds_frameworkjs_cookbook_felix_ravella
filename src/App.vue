
<template>
  <h1>Recipe Book</h1>
  <!-- New recipe form -->
  <form @submit.prevent="addRecipe">
    <input type="text" placeholder="Add a new recipe..." v-model="newRecipeTitle">
    <button type="submit" :disabled="newRecipeTitle === ''">Add</button>
  </form>

  <!-- List of Recipes + Buttons for Edit & Delete-->
  <RecipeButton v-for="item,index of recipes" 
    :key="index"
    :recipeIndex="index"
    :title="item.title"
    @requestEdit="(recipeIndex) => selectedRecipe = recipeIndex"
    @requestDelete="(recipeIndex) => recipes.splice(recipeIndex, 1)"
    />
  <br>

  <!-- Recipe view and edition; only displayed if a recipe is selected by clicking on 'Edit' -->
  <RecipeDetail v-if="selectedRecipe !== null"
    :key="selectedRecipe"
    :recipeIndex="selectedRecipe"
    :initialData="recipes[selectedRecipe]"
    @dataChanged="onRecipeDataChanged"
  />

  <ShoppingList />
    
</template>

<script>
import RecipeButton from './components/RecipeButton.vue'
import RecipeDetail from './components/RecipeDetail.vue'
import ShoppingList from './components/ShoppingList.vue'

export default {
  name: 'App',
  components:{
    RecipeButton,
    RecipeDetail,
    ShoppingList
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
    },
    onRecipeDataChanged(index, data){
      this.recipes[index] = {...data};
    }
  }
  
}
</script>


<style scoped>
</style>
