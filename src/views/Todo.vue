<template>
  <div class="container">
    <h1>todo list</h1>
    <div class="todo_box">
      <div class="todo_input">
        <input type="text" name id v-model="addText"/>
        <button @click="addTodo">+</button>
      </div>
      <div class="todo_list">
        <ul>
          <li v-for="todo in todoList" :key="todo.content">
            <input type="checkbox" name id />
            <label for></label> {{todo.content}}
            <button>X</button>
          </li>
          
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
  data() {
    return {
      addText: "",
      todoList: []
    };
  },
  methods: {
    addTodo() {
      this.todoList.push({
        content:this.addText,
        compoleted:false
      });
      this.addText=''
      console.log(this.todoList)
    }
  },
  watch:{
    addText(){
      console.log(this.addText)
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
