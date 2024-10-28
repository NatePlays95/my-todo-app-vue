<script>
export default {
  data() {
    return {
      msg: 'Hello World!',
      newTask: "",
      taskList: ["task1", "task2"]
    }
  },

  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.taskList.push(this.newTask);
        this.newTask = "";
      }
    },
    deleteTask(index) {
      this.taskList.splice(index, 1);
    }
  }
}
</script>

<template>
  <h1>To-Do List</h1>
  <div>
    <input v-model="newTask">
    <button @click="addTask()">Add</button>
  </div>

  <ul>
    <li v-for="(task, index) in taskList">
      {{task}}
      <button v-on:click="deleteTask(index)">Delete</button>
    </li>
  </ul>
</template>