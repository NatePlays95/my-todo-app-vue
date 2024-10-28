<script>
import './TodoListApp.css'
import TaskCard from './components/TaskCard.vue'

export default {
    components: {
        TaskCard
    },

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
    <div className="app-container">
        <div className="task-column">
            <h2>To-Do List</h2>

            <TaskCard 
            v-for="(task, index) in taskList"
            :key="index"
            :task="task"
            :index="index"
            @delete-task="deleteTask"
            ></TaskCard>

           
            <input 
            v-model="newTask" 
            className='add-task-input' 
            type="text"
            placeholder="Add a new task"
            >
            <button className='add-task-button' @click="addTask">Add Task</button>
            
        </div>
    </div>
</template>