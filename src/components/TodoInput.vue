<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
     <img src="@/assets/img/plus.png" alt="추가하기">
    </span>
  </div>
</template>

<script>
export default {
  
  data: function() {
    return{
      newTodoItem:""
    }
  },
  methods:{
    addTodo: function(){
      //console.log(this.newTodoItem)
      if(this.newTodoItem !== ''){
      let obj = {completed:false, item:this.newTodoItem}
      //localStorage.setItem(this.newTodoItem, obj)
      localStorage.setItem(this.newTodoItem, JSON.stringify(obj))
      this.clearInput()
      }
    },
    clearInput: function(){
      this.newTodoItem = ''
    }
  }
}
</script>

<style>

</style>