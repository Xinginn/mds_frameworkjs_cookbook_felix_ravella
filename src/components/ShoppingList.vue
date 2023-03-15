<template>
  <div class="shopping-list">

    <h1 class="shopping-list-title">Shopping List</h1>

    <ShoppingItem v-for="item,index of mutableData" 
      :key="index"
      :ingedientIndex="index" 
      :ingredient="item"
      @boughtChanged="onItemBoughtChanged"
    />

    <!-- Buttons for list check handling -->
    <div class="shopping-list-actions">
      <button type="button" @click="checkAll">Check all</button>
      <button type="button" @click="clearAllChecked">Clear checked items</button>
      <button type="button" @click="clearAll">Clear all</button>
    </div>
  </div>
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
    },
    checkAll(){
      this.mutableData.map(item => item.bought = true);
      this.$emit('dataChanged', this.mutableData);
    },
    clearAll(){
      this.$emit('dataChanged', []);
    },
    clearAllChecked(){
      this.mutableData = this.mutableData.filter((item) => {
        return item.bought === false
      })
      this.$emit('dataChanged', this.mutableData);
    }
  }
}
</script>