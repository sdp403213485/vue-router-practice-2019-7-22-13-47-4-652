<template>
  <div id="app">
    <h2>
      Vue To Do List
      Simple Todo List with adding and filter by diff status.
    </h2>
    <create @addNewToDo="handleAdd" />
    <div id="list">
      <ul>
        <li v-for="(item,index) in filteredTodoList" :key="index">{{item.content}}</li>
      </ul>
    </div>
    <div class="filter">
      当前状态：{{this.currentFilter}}
      <button @click="filterActive('active')">Active</button>
      <button @click="filterActive('completed')">Completed</button>
    </div>
  </div>
</template>

<script>
import create from "./components/CreateForm.vue";

export default {
  name: "app",
  components: {
    create
  },
  data: function() {
    return {
      /**
       * 定义了 todo item 中属性为 {content:'吃饭',status:'active'}
       * 定义了 todo 的两种状态 completed、active，默认为 active
       */
      todoList: [
        { content: "1", status: "active" },
        { content: "2", status: "active" },
        { content: "3", status: "active" }
      ],
      currentFilter: "active"
    };
  },
  computed: {
    filteredTodoList: function() {
      let filteredList = [];
      for (let index = 0; index < this.todoList.length; index++) {
        const element = this.todoList[index];
        if (element.status === this.currentFilter || this.status === "all") {
          filteredList.push(element);
        }
      }
      return filteredList;
    }
  },
  methods: {
    handleAdd: function(inputtingText) {
      this.todoList.push({
        content: inputtingText,
        status: "active"
      });
    },
    filterActive: function(status) {
      this.currentFilter = status;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.items {
  list-style: none;
  text-align: left;
  line-height: 30px;
}

.items li.completed {
  text-decoration: line-through;
}

.filter a {
  margin: 0 10px;
  line-height: 30px;
}

.filter a.active {
  color: #f60;
  border: 1px solid #ccc;
  border-radius: 2px;
  padding: 3px;
  cursor: pointer;
}
</style>
