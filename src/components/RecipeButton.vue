<template>
  <span>{{title}}</span>
  <button type="button" @click="() => $emit('requestEdit', recipeIndex)">Edit</button>
  <button type="button" @click="() => $emit('requestDelete', recipeIndex)">Delete</button>
</template>

<script lang="ts">
export default {
  name:'RecipeButton',
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