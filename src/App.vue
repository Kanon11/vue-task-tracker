<template>
  <div class="container">
    <HeaderComponent
      title="Task Tracker"
      :showAddTask="showAddTask"
      @main-toggle="toggleButton()"
    ></HeaderComponent>
    <add-task @add-task="AddTask($event)" v-if="showAddTask"></add-task>
    <tasks-component
      :tasks="taskList"
      @main-delete="DeleteTask($event)"
      @main-toggle="toggleRemider($event)"
    ></tasks-component>
  </div>
</template>

<script>
import axios from "axios";
import HeaderComponent from "./components/Header.vue";
import TasksComponent from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";
export default {
  name: "App",
  components: {
    HeaderComponent,
    TasksComponent,
    AddTask,
  },
  data() {
    return {
      taskList: [],
      showAddTask: true,
      buttonColoer: "green",
      btntitle: "Add Task",
    };
  },
  methods: {
    async DeleteTask(id) {
      if (confirm("Are you sure!!!"))
        try {
          await axios
            .post(`http://localhost:3000/tasks/delete`, { id: id })
            .then((response) => {
              if (response.data.statuscode == 200) {
                this.getAllTask();
              } else {
                alert("delete is not success, try another time");
              }
            });
        } catch (error) {
          alert(error);
        }
    },
    async toggleRemider(id) {
      await axios
        .post(`http://localhost:3000/tasks/toggle`, { id: id })
        .then((response) => {
          if (response.data.statuscode == 200) {
            this.getAllTask();
          } else {
            alert("toggle failed");
          }
        });
    },
    async getAllTask() { //kc
      try {
        const gettaskListUrl = `http://localhost:3000/tasks`;
        axios.get(gettaskListUrl).then((response) => {
          if (response.data.statuscode == 200) {
            this.taskList = response.data.data;
          }
        });
      } catch (e) {
        alert(e);
      }
    },
    async AddTask(data) {
      try {
        await axios
          .post(`http://localhost:3000/tasks/create`, data)
          .then((response) => {
            if (response.data.statuscode == 200) {
              this.getAllTask();
            } else {
              alert("Task is not inserted");
            }
          });
      } catch (error) {
        alert(error);
      }
    },
    toggleButton() {
      this.showAddTask = !this.showAddTask;
    },
  },
  created() {
    this.getAllTask();
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
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
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
