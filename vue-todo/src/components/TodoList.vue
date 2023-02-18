<template>
  <div>
    <ul>
      <li  v-for="(todoItems,index) in todoItems" v-bind:key="todoItems" class="shadow">
        {{ todoItems }}
        <span class="removeBtn" v-on:click="removeTodo(todoItems,index)">delete</span>
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
    removeTodo: function(todoItems, index ){
      console.log(todoItems, index);
      localStorage.removeItem(todoItems)
      this.todoItems.splice(index, 1)
    }
  },
  created: function(){
    if(localStorage.length > 0){
      for(var i = 0; i < localStorage.length; i++){
        if(localStorage.key(i) !== "logolevel:webpack-dev-server")
        this.todoItems.push(localStorage.key(i))
        // console.log(localStorage.key(i));
      }
    }  
  }
}
</script>

<style>
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
.ckeckBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
  cursor: pointer;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

</style>