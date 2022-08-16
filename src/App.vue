<template>
  <div class="container">
    <HeaderComponent title="Task Tracker" :showAddTask="showAddTask" @main-toggle="toggleButton()"></HeaderComponent>
    <add-task @add-task="AddTask($event)" v-if="showAddTask"></add-task>
    <tasks-component :tasks="taskList" @main-delete="DeleteTask($event)" @main-toggle="toggleRemider($event)"></tasks-component>
  </div>
</template>

<script>
import HeaderComponent from "./components/Header.vue";
import TasksComponent from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";
export default {
  name: "App",
  components: {
    HeaderComponent,
    TasksComponent,
    AddTask
  },
  data() {
    return {
      taskList: [],
      showAddTask:true,
      buttonColoer:'green',
      btntitle:'Add Task'
    };
  },
  methods:{
    DeleteTask(id){
      if(confirm("Are you sure!!!"))
      this.taskList=this.taskList.filter((task)=>task.id!==id);
    },
    toggleRemider(id){
      // console.log(id);
      this.taskList=this.taskList.map((task)=>task.id===id?{...task,reminder:!task.reminder}:task)
    },
    AddTask(data){
      console.log(data);
    },
    toggleButton(){
      this.showAddTask=!this.showAddTask;

    }
  }
  ,
  created() {
    this.taskList = [
      {
        id: "1",
        text: "Doctors Appointment",
        day: "March 5th at 2:30pm",
        reminder: true,
      },
      {
        id: "2",
        text: "Meeting with boss",
        day: "March 6th at 1:30pm",
        reminder: true,
      },
      {
        id: "3",
        text: "Food shopping",
        day: "March 7th at 2:00pm",
        reminder: false,
      },
    ];
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
