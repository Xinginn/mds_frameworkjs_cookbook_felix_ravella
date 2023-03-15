
<template>
  <h1>Recipe Book</h1>

shoppingList: {{ shoppingList }}

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
    @addToList="onAddToListClicked"
  />

  <ShoppingList :ingredients="shoppingList"/>
    
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
          description: "A mediocre specialty from Britain, with cabbage and other vegetables.",
          ingredients: [
            "1 cabage",
            "3 potatoes",
            "2 onions"
          ]
        },
      ],
      selectedRecipe: null,
      newRecipeTitle: "",
      shoppingList: []
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
      this.selectedRecipe = null;
    },
    onAddToListClicked(index){
      // create a new array of objects with label(ingredient) and bought(default as false) rom the ingredient list
      const addedIngredients = this.recipes[index].ingredients.reduce((stack, current)=> {
        return [...stack, {label: current, bought: false}]
      }, []);
      // then concats it with the current shoppingList
      this.shoppingList = this.shoppingList.concat(addedIngredients);
      this.selectedRecipe = null;
    }
  }
}
</script>


<style scoped>
</style>
