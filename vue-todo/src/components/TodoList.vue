<template>
  <div>
    <ul>
      <li v-for="todoItems in todoItems" v-bind:key="todoItems">
        {{ todoItems }}
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

</style>