<template>
  inside shopping list
  <br>
  ingredients: {{ ingredients }}
</template>

<script>
export default {
  name: 'ShoppingList',
  props: {
    ingredients: Array
  },
  emits:[
  ],
}
</script>