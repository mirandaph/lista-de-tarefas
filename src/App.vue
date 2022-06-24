<template>
  <div class="container">
    <HeaderVVue :showAddTask="showAddTask" @show-add-task="showAdd" title="Lista"/>
    <div v-if="showAddTask">
      <AddTaskVue @add-task="addingTask"/>
    </div>
    <TasksVue @delete-task="deleteTask" v-bind:tasks="tasks" />
  </div>
</template>

<script>
import HeaderVVue from "./components/HeaderV.vue";
import TasksVue from "./components/Tasks.vue";
import AddTaskVue from "./components/AddTask.vue";
import json from "/db.json"

export default {
  name: "App",
  components: {
    HeaderVVue,
    TasksVue,
    AddTaskVue,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    async addingTask(task) {
      const dataJson = JSON.stringify(task)

      const req = await fetch("http://localhost:3000/tasks", {
          method: 'POST',
          headers: { 'Content-Type': 'application/json'},
          body: dataJson
          })

      const res = await req.json()

      this.tasks = [...this.tasks, task]
    
    },
    showAdd(){
      this.showAddTask = !this.showAddTask
    },
    async deleteTask(id){
      this.tasks = this.tasks.filter((task) => task.id !== id)

      // DELETE
      
      const req = await fetch(`http://localhost:3000/tasks/${id}`, {
        method: 'DELETE',
      })

      const res = await req.json()
    },
    async togglePriority(id, priority, text, task, proxy){
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, priority: !task.priority} : task)
    },
  },
created() {
    this.tasks = json.tasks
  },
};

</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Raleway', sans-serif;
  font-weight: 400;
  background-color: rgb(21, 40, 75);
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  background-color: steelblue;
  padding: 30px;
  margin-top: 120px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
