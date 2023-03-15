<template>
  <br>
  <ShoppingItem v-for="item,index of mutableData" 
    :key="index"
    :ingedientIndex="index" 
    :ingredient="item"
    @boughtChanged="onItemBoughtChanged"
  />
</template>

<script>
import ShoppingItem from './ShoppingItem.vue'

export default {
  name: 'ShoppingList',
  components: {
    ShoppingItem
  },
  props: {
    initialData: Array
  },
  mounted(){
    this.mutableData = [...this.initialData]
  },
  emits:[
    'dataChanged',
  ],
  data(){
    return {
      mutableData: []
    }
  },
  methods: {
    onItemBoughtChanged(index, value){
      this.mutableData[index].bought = value;
      this.$emit('dataChanged', this.mutableData);
    }
  }
}
</script>