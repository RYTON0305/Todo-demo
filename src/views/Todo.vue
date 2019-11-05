<template>
  <div class="todo_box">
    <h1 class="header">Todo List</h1>
    <div class="todo_input">
      <input
        class="input_box"
        placeholder="请输入Todo"
        type="text"
        name
        id
        v-model="addText"
        @keypress.enter="addTodo"
      />
      <button @click="addTodo">+</button>
    </div>
    <div class="todo_list_box">
      <ul class="todo_list">
        <li class="list_item" v-for="(todo,index) in todoList" :key="index">
          <input class="toggle" :id="'todo'+index" type="checkbox" v-model="todo.completed" />
          <label :for="'todo'+index" class="toggleR">
            <i class="iconfont icongou" :class="{icon_completed:todo.completed}"></i>
          </label>
          <label
            :for="'todo'+index"
            class="toggleBox"
            :class="{todo_completed:todo.completed}"
          >{{todo.content}}</label>
          <a class="delBtn" @click="delTodo(index)">×</a>
        </li>
      </ul>
    </div>
    <div class="todo_count">
      <span>一共有{{todoList.length}}个todo</span>
      <a href="#" @click="clearTodo">清除所有Todo</a>
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
    //console.log("test");
    if (todoList) {
      // //console.log("我找到辣");
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
      //console.log(this.todoList);
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
    //   //console.log(this.addText);
    // },
    todoList: {
      deep: true,
      handler: function(newValue, oldValue) {
        //console.log(newValue);
        this.saveStorage();
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
* {
  box-sizing: border-box;
}
.header {
  padding: 0;
  margin: 0;
  text-align: center;
}
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
button {
  /* margin: 0; */
  /* padding:0; */
  outline: none;
  /* line-height: 1; */
}
body,
html {
  line-height: normal;
}

input {
  outline: 0;
  line-height: 1;
}

body {
  /* font: 14px "Helvetica Neue", Helvetica, Arial, sans-serif;
  line-height: 1.4em;
  background: #f5f5f5;
  color: #4d4d4d;
 
  margin: 0 auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-weight: 300;
  transition: all 0.4s ease; */
  min-width: 230px;
  max-width: 550px;
  margin: 0 auto !important;
  transition: ease 0.4s all;

}
body:hover {
  background-color: #cc9a9a;
}
body:hover .header {
  color: #fff
}
.todo_box {
  position: relative;
  /* width: 550px;
  max-width: 550px;
  min-width: 230px; */
  /* margin: 130px 0  40px 0; */
  /* box-shadow: 0 0 10px #ddd; */

  background: #fff;
  margin: 130px 0 40px 0;
  position: relative;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
  /* font: 14px "Helvetica Neue", Helvetica, Arial, sans-serif; */
  /* line-height: 1.4em; */
  /* background: #f5f5f5; */
  /* color: #4d4d4d;
  min-width: 230px;
  max-width: 550px;
  margin: 0 auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-weight: 300;
  transition: all 0.5s ease; */
}

.header {
  position: absolute;
  top: -140px;
  font-size: 100px;
  font-weight: 400;
  color: #cc9a9a;
  text-align: center;
  width: 100%;
  transition: ease 0.4s all;
}
.todo_input {
  width: 100%;
  position: relative;
}
.todo_input .input_box {
  width: 100%;
  height: 64px;
  padding: 10px 0 10px 60px;
  border: none;
  font-size: 20px;
  border-bottom: 1px solid #ddd;
}
.input_box::placeholder {
  font-style: italic;
  font-weight: 400;
  color: #ccc;
}
.todo_input:hover > button {
  background-color: #cc9a9a;
  color: #fff;
}
.todo_input button {
  /* position: absolute;
  bottom:0;
  right: 25px;
  
  border: 0;
  background:none;
  padding: 0;
  font-size: 30px;
  color: #cc9a9a;
  width: 40px;
  height: 40px;
  line-height: 40px;
  margin: 12px 0; */
  position: absolute;
  top: 0;
  right: 25px;
  bottom: 0;
  width: 40px;
  height: 40px;
  padding: 0;
  font-size: 30px;
  margin: auto 0;
  color: #cc9a9a;
  -webkit-transition: all 0.4s ease-out;
  transition: all 0.4s ease-out;
  border-radius: 5px;
  cursor: pointer;
  z-index: 999;
  border: none;
  background: none;
  line-height: 40px;
  font-family: "Times New Roman", Times, serif;
  font-weight: 900;
}
.todo_list_box {
  /* width: 100%; */
}
.todo_list {
  /* width: 100%; */
}
.list_item {
  position: relative;
  height: 60px;
  border-bottom: 1px solid #ddd;
  /* width: 100%; */
  /* border: 2px solid #ccc; */
}
.list_item .toggleBox {
  display: block;
  width: 100%;
  height: 100%;
  background-color: white;
  padding: 10px 10px 10px 60px;
  font-size: 20px;
  line-height: 40px;
  cursor: pointer;
  transition: all 0.4s ease;
}
.toggleR {
  display: inline-block;
  position: absolute;
  top: 10px;
  left: 10px;
  height: 40px;
  width: 40px;
  padding: 10px 0;
  border-radius: 50%;
  cursor: pointer;
  background-color: white;
  border: 1px solid #ccc;
  line-height: 20px;
  text-align: center;
  /* font-size: 20px; */
  /* font-weight: 900; */

  /* line-height: 40px; */
}
.icongou {
  font-size: 30px;
  color: #fff;
  transition: all 0.4s ease;
}
.icon_completed {
  color: lightgreen;
}
.toggle {
  /* position: absolute;
  top:0;
  left: 0px;
  height: 100%;
  width: 40px;
  padding:10px 0;
  border-radius:50%;
  cursor: pointer; */
  display: none;
}
.todo_completed {
  color: #ccc;
  text-decoration: line-through;
}
.delBtn {
  display: inline-block;
  position: absolute;
  right: 10px;
  top: 10px;
  width: 40px;
  height: 40px;
  font-size: 30px;
  line-height: 35px;
  vertical-align: middle;
  text-align: center;
  cursor: pointer;
  color: #cc9a9a;
  transition: all ease 0.4s;
  z-index: -1;
  /* visibility: hidden; */
  opacity: 0;
}
.list_item:hover > .delBtn {
  opacity: 1;
  z-index: 1;
}
.todo_count {
  width: 100%;
  height: 50px;
  font-size: 14px;
  line-height: 50px;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2), 0 8px 0 -3px #f6f6f6,
    0 9px 1px -3px rgba(0, 0, 0, 0.2), 0 16px 0 -6px #f6f6f6,
    0 17px 2px -6px rgba(0, 0, 0, 0.2);
}
.todo_count span {
  float: left;
  padding-left: 10px;
}
.todo_count a {
  float: right;
  color: #bbb;
  padding-right: 10px;
}
</style>