<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <div>TodoApp</div>
  <div>
    <div>タスクの追加</div>
    <input v-on:keyup.enter="addTask" v-model="newTask" type="text" />
    <button @click="addTask">追加</button>
  </div>
  <div>
    <p>タスク一覧</p>
    <div v-for="todo in todos" :key="todo.id" class="taskItem">
      <input type="checkbox" v-model="todo.isCompleted" @change="saveTask" />
      <p :class="{ complete: todo.isCompleted }">{{ todo.task }}</p>
      <button @click="deleteTask(todo)">削除</button>
    </div>
  </div>
</template>

<script>
// import { onMounted } from "vue";
import { reactive, ref } from "@vue/reactivity";
export default {
  name: "App",
  setup() {
    let todos = reactive([
      {
        task: "Ruby",
        isCompleted: false,
      },
      {
        task: "PHP",
        isCompleted: false,
      },
      {
        task: "Vue.js",
        isCompleted: false,
      },
    ]);
    const newTask = ref();

    // onMounted(() => {
    //   loadTodo();
    // });

    const addTask = () => {
      if (newTask.value === "") return;
      todos.push({ task: newTask.value, isCompleted: false });
      newTask.value = "";
      saveTask();
    };

    const deleteTask = (todo) => {
      const index = todos.indexOf(todo);
      todos.splice(index, 1);
    };

    const saveTask = () => {
      localStorage.setItem("todos", JSON.stringify(todos));
    };

    // const loadTodo = () => {
    //   todos = JSON.parse(localStorage.getItem("todos"));
    //   console.log(todos);
    //   if (!todos) {
    //     todos = [];
    //   }
    // };

    return { todos, addTask, deleteTask, newTask, saveTask };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.complete {
  text-decoration: line-through;
  color: #ddd;
}

.taskItem {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
