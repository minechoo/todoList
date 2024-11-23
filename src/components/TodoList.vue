<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
        <button class="checkBtn">
        <img src="@/assets/img/check.png" 
        v-bind:class="{checkBtnCompleted: todoItem.completed}"
        v-on:click="toggleComplete(todoItem, index)">
        </button>
        <span v-bind:class="{textCompleted: todoItem.completed}">{{todoItem.item}}</span>
        <button v-on:click="removeTodo(todoItem, index)" class="removeBtn"><img src="@/assets/img/trash.png"></button>
      </li>
    </ul>
    
  </div>
</template>

<script>
export default {
  data: function(){
    return{
      todoItems: []
    }
  },
  methods: {
    removeTodo: function(todoItem, index){
      console.log(todoItem, index)
      localStorage.removeItem(todoItem)
      this.todoItems.splice(index, 1)
    },
    toggleComplete: function(todoItem){
      todoItem.completed = !todoItem.completed
      //로컬스토리지 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    }
  },
  created: function(){
    if(localStorage.length > 0){
      for(let i = 0; i < localStorage.length; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))))
          //this.todoItems.push(localStorage.key(i))
        }     
      }
    }
  }
}
</script>

<style>

</style>