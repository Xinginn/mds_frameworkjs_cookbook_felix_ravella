<template>
  <div class="recipe">
    <div class="recipe-title">{{title}}</div>
    <div class="recipe-actions">
      <button class="recipe-edit-button" type="button" @click="() => $emit('requestEdit', recipeIndex)">Edit</button>
      <button class="recipe-delete-button" type="button" @click="() => $emit('requestDelete', recipeIndex)">Delete</button>
    </div>
    <br>
  </div>
</template>

<script>
export default {
  name: 'RecipeButton',
  props: {
    recipeIndex: Number,
    title: String
  },
  emits:[
    'requestEdit',
    'requestDelete',
  ]
}
</script>