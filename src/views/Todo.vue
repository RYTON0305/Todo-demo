<template>
  <div class="container">
    <h1>todo list</h1>
    <div class="todo_box">
      <div class="todo_input">
        <input
          placeholder="请输入Todo"
          type="text"
          name
          id
          v-model="addText"
          @keypress.enter="addTodo"
        />
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
        <span>一共有{{todoList.length}}个todo</span>
        <a href="#" @click="clearTodo">清除所有Todo</a>
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
  mounted() {
    let todoList = JSON.parse(window.localStorage.getItem("todoList"));
    console.log("test");
    if (todoList) {
      // console.log("我找到辣");
      this.todoList = todoList;
    }
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
    },
    clearTodo() {
      this.todoList = [];
    },
    saveStorage() {
      window.localStorage.setItem("todoList", JSON.stringify(this.todoList));
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
        this.saveStorage();
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
