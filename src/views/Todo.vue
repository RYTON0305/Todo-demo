<template>
  <div class="container">
    <h1>todo list</h1>
    <div class="todo_box">
      <div class="todo_input">
        <input type="text" name id /><button>+</button>
      </div>
      <div class="todo_list">
        <ul>
          <li>list</li>
          <li>list</li>
          <li>list</li>
          <li>list</li>
        </ul>
      </div>
      <div class="todo_count">
        <span>一共有*个todo</span>
        <span>清除所有todo</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data(){
    return{
      addText:'',
      todoList:[]
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
