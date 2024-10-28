<script>
export default {
  data() {
    return {
      newTask: "",
      taskList: []
    }
  },

  mounted() { //this runs when the page (or component) loads 
    this.loadTaskList();
  },

  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.taskList.push(this.newTask);
        this.newTask = "";

        this.saveTaskList();
      }
    },

    deleteTask(index) {
      this.taskList.splice(index, 1);

      this.saveTaskList();
    },

    saveTaskList() {
        const taskListString = JSON.stringify(this.taskList);
        if (taskListString) {
            localStorage.setItem("taskList", taskListString);
            console.log("saved list: ", taskListString);
        }
    },

    loadTaskList() {
        const savedTaskListString = localStorage.getItem("taskList");
        if (savedTaskListString) {
            const newTaskList = JSON.parse(savedTaskListString);
            this.taskList = [...newTaskList];
            console.log("loaded list: ", savedTaskListString);
        } else {
            console.log("no data to load");
        }
        
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