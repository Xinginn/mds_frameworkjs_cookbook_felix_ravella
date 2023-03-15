<template>
  <form @submit.prevent="saveChanges">
    <input type="text" v-model="mutableData.title">
    <br>
    <textarea v-model="mutableData.description"
      rows="10" cols="40"
    >
    </textarea>
    <br>
    <template v-for="item,index of mutableData.ingredients" :key="index">
      <input v-model="mutableData.ingredients[index]">
      <br>
    </template>
    <button type="submit">Save</button>
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
    'dataChanged'
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
      }
    }
  },
  methods: {
    saveChanges(){
      this.$emit('dataChanged', this.recipeIndex, this.mutableData)
    }
  }
}
</script>