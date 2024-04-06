<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import { ref, onMounted } from "vue";

const todoList = ref([]);
const taskText = ref("");

const addTask = () => {
  if (taskText.value.trim() !== "") {
    todoList.value.push(taskText.value);
    taskText.value = "";
  }

  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

const deleteTask = (index) => {
  todoList.value.splice(index, 1);
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

const loadTasks = () => {
  const tasks = localStorage.getItem("todoList");
  if (tasks) {
    todoList.value = JSON.parse(tasks);
  }
};
onMounted(() => {
  loadTasks();
});
</script>

<template>
  <div>
    <img alt="Asem logo" class="logo" src="../public/favicon.png" />
    <div class="main" dir="ltr">
      <div class="task-input">
        <form @submit.prevent="addTask">
          <input
            type="text"
            class="task-text"
            v-model="taskText"
            placeholder="type a task"
          />
          <button class="add-task-btn" type="submit">Add Task</button>
        </form>
      </div>
      <div class="todo-list">
        <ul>
          <li v-for="(task, index) in todoList" :key="index">
            <div style="width: 100%" class="list-template">
              <span>
                {{ index + 1 }}.
                {{ task }}
              </span>
              <a href="#" @click="deleteTask" class="delete-btn"><i>x</i></a>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.main {
  display: grid;
  place-items: center;
  height: auto;
  font-size: calc(10px + 2vmin);
  color: white;
  width: 60vw;
  background-color: #282c34;
  border: #282c34;
  box-shadow: 0 0 1px 3px #282c34;
}
.task-input {
  width: 100%;
}
.task-input form {
  width: 100%;
  padding: 1rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-items: center;
  align-items: center;
}
.task-text {
  width: 100%;
  margin-inline: 1em;
  font-size: 0.6em;
  border: none;
  border-radius: 0.5em;
  box-shadow: 0 0 0.1em 0.5em #646cff;
  transition: box-shadow 300ms;
  float: left;
  padding: 0.5em;
}
.add-task-btn {
  float: left;
  padding: 0.5em;
  margin-inline: 3rem;
  border: none;
  border-radius: 0.5em;
  background-color: #646cff;
  color: white;
  font-size: 0.6em;
  box-shadow: 0 0 0.1em 0.08em #646cff;
  transition: box-shadow 300ms;
}
.todo-list {
  width: 100%;
  border-radius: 0.5em;
}
.todo-list ul {
  color: white;
  list-style: none;
  display: inline;
}
.todo-list ul li {
  padding: 0.4em;
  margin: 0.8em;
  background-color: #646cff;
  border-radius: 0.5em;
  box-shadow: 0 0 0.1em 0.5rem #646cff;
  transition: box-shadow 300ms;
}
.delete-btn {
  color: red;
  font-size: 1.9em;
}
.list-template {
  display: grid;
  grid-template-columns: 100px 100px 10px;
  grid-template-rows: 10px 10px;
  justify-items: start; /* Align items along the row axis */
  align-items: center; /* Align items along the column axis */
  justify-content: space-around; /* Align tracks along the row axis */
  align-content: space-around; /* Align tracks along the column axis */
  height: 30px; /* Just for demonstration */
  font-size: 1rem;
}
.list-template span {
  grid-column: 1 / 3;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Noto Sans Arabic", sans-serif;
}
</style>
