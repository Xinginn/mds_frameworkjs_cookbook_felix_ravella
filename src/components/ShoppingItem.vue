<template>
  <div class="shopping-list-item ">
    <input type="checkbox" v-model="bought" @change="test">
    <span>{{ ingredient.label }}</span>
  </div>
</template>

<script>
export default {
  name: 'ShoppingItem',
  props: {
    ingedientIndex: Number,
    ingredient: Object
  },
  emits:[
    'boughtChanged'
  ],
  mounted(){
    this.bought = this.ingredient.bought;
  },
  data(){
    return {
      bought: false
    }
  },
  methods: {
    test(){
      this.$emit('boughtChanged', this.ingedientIndex, this.bought)
    }
  }
}
</script>