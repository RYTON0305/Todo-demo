<template>
  <div class="container">
    <h1>todo list</h1>
    <div class="todo_box">
      <div class="todo_input">
        <input type="text" name id v-model="addText" @keypress.enter="addTodo" />
        <button @click="addTodo">+</button>
      </div>
      <div class="todo_list">
        <ul>
          <li v-for="(todo,index) in todoList" :key="index">
            <input type="checkbox" v-model="todo.completed" name id />
            <label for></label>
            {{todo.content}}
            <button @click="delTodo(index)">X</button>
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
      todoList: [
        {
          content: "吃饭",
          completed: true
        },
        {
          content: "睡觉",
          completed: false
        },
        {
          content: "洗澡",
          completed: false
        }
      ]
    };
  },
  methods: {
    addTodo() {
      if (this.addText === "") {
        alert("请输入Todo");
        return;
      }

      this.todoList.push({
        content: this.addText,
        completed: false
      });
      this.addText = "";
      console.log(this.todoList);
    },
    delTodo(index) {
      this.todoList.splice(index, 1);
    }
  },
  watch: {
    // addText() {
    //   console.log(this.addText);
    // },
    todoList: {
      deep: true,
      handler: function(newValue, oldValue) {
        console.log(newValue);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
