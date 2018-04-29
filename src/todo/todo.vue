
<template>
  <section class="real-app">
      <input type="text" 
             class="addInput"
             autofocus="autofocus"
             placeholder="接下来要做什么"
             @keyup.enter="addTodo"
      >
      
      <APP_Item :todo="todo"
                 v-for="todo in filteredTodos"
                 :key="todo.id"
                 @del="deleteTodo"
      ></APP_Item>

      <APP_Tabs 
      :filter="filter"
      @toggle="toggleFilter"
      @clearAllCompleted="clearAllCompleted"

      ></APP_Tabs>
  </section>
</template>

<script>
import APP_Item from "./item.vue";
import APP_Tabs from "./tabs.vue";

let id = 0;

export default {
  data() {
    return {
      todos: [],
      filter: "all"
    };
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      }
      const completed = this.filter === "completed";
      // 将todos数组中，completed为true的值过滤出来，并返回一个新数组
      return this.todos.filter(todo => completed === todo.completed);
    }
  },
  methods: {
    addTodo(e) {
      if (e.target.value.trim()) {
        this.todos.unshift({
          id: id++,
          content: e.target.value.trim(),
          completed: false
        });
        e.target.value = "";
      } else {
        alert("傻X，输入不能为空 !-_-");
      }
    },
    toggleFilter(state) {
      this.filter = state;
    },
    deleteTodo(id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1);
    },
    clearAllCompleted(){
        this.todos = this.todos.filter(todo => todo.completed === false)
    }
  },
  components: {
    APP_Item,
    APP_Tabs
  }
};
</script>

<style lang="less" scoped>
.real-app {
  width: 600px;
  margin: 0 auto;
  box-shadow: 0 0 5px #666;
}
.addInput {
  position: relative;
  margin: 0;
  width: 100%;
  font-size: 24px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1.4em;
  border: 0;
  outline: none;
  color: inherit;
  box-sizing: border-box;
  font-smoothing: antialiased;
  padding: 16px 16px 16px 36px;
  border: none;
  box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
}
</style>

