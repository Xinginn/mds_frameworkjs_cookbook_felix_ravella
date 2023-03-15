
<template>


  <div class="main">
    <h1 class="main-title">Recipe Book</h1>

    <!-- New recipe form -->
    <form class="new-recipe-form" @submit.prevent="addRecipe">
      <input class="recipe-title-input" type="text" placeholder="Add a new recipe..." v-model="newRecipeTitle">
      <button class="recipe-create-button" type="submit" :disabled="newRecipeTitle === ''">Add</button>
    </form>

    <div class="recipe-book">
      <!-- List of Recipes + Buttons for Edit & Delete-->
      <RecipeButton v-for="item,index of recipes" 
        :key="index"
        :recipeIndex="index"
        :title="item.title"
        @requestEdit="(recipeIndex) => selectedRecipe = recipeIndex"
        @requestDelete="(recipeIndex) => recipes.splice(recipeIndex, 1)"
        />
    </div>

    <!-- Recipe view and edition; displayed only if a recipe is selected by clicking on 'Edit' -->
    <RecipeDetail v-if="selectedRecipe !== null"
      :key="selectedRecipe"
      :recipeIndex="selectedRecipe"
      :initialData="recipes[selectedRecipe]"
      @dataChanged="onRecipeDataChanged"
      @addToList="onAddToListClicked"
    />

    <ShoppingList 
      :initialData="shoppingList"
      :key="shoppingRefresh"
      @dataChanged="onShoppingListChanged"
    />
  </div>
    
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
      shoppingList: [],
      shoppingRefresh: 0, // used as key to ensure refresh of ShoppingList component
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
      this.shoppingRefresh += 1;
    },
    onShoppingListChanged(data){
      this.shoppingList = data;
      this.shoppingRefresh += 1;
    }
  }
}
</script>


<style scoped>
</style>
