<template>
  <div>
    <ul>
      <li  v-for="(todoItem,index) in todoItems" v-bind:key="todoItem.item" class="shadow">
        <p class="checkBtn" 
          v-bind:class="{checkBtnCompleted:todoItem.completed}" 
          v-on:click="toggleComplte(todoItem,index)">
          check
        </p>
        <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem,index)">delete</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function(){
    return { 
      todoItems: []
    }
  },
  methods: {
    removeTodo: function(todoItem, index ){
      console.log(todoItem, index);
      localStorage.removeItem(todoItem)
      this.todoItems.splice(index, 1)
    },
    toggleComplte: function(todoItem,index){
      console.log(todoItem, index);
      todoItem.completed = !todoItem.completed;
      // localStorage deta update
      localStorage.removeItem(todoItem.item)
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem))
    }
  },
  created: function(){
    if(localStorage.length > 0){
      for(var i = 0; i < localStorage.length; i++){
        if(localStorage.key(i) !== "logolevel:webpack-dev-server")
        this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))))
        console.log(JSON.parse(localStorage.getItem(localStorage.key(i))));
        // this.todoItems.push(localStorage.key(i))
        // console.log(localStorage.key(i));
      }
    }  
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: .5rem 0;
  padding: 0 .9rem;
  background:#fff;
  border-radius: 5px;
}
.checkBtn {
  line-height: 18px;
  color: #62acde;
  margin-right: 5px;
  border: 1px solid #62acde;
  display: inline-block;
  cursor: pointer;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
  cursor: pointer;
}
.checkBtnCompleted {
  color: #b3adad;
  border: 1px solid #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

</style>