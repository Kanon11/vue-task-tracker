<template>
  <div v-for="task in tasks" :key="task.id">
    <task-component @task-delete="td($event)" @toggleemit="funtoggleemit($event)" :task="task"></task-component>
  </div>
</template>
<script>
import TaskComponent from "./Task.vue";
export default {
  components: {
    TaskComponent,
  },
  name: "TasksComponent",
  props: {
    tasks: Array,
  },
  emits:['main-delete','main-toggle'],
  methods:{
    td(id){
        this.$emit('main-delete',id);
    },
    funtoggleemit(id){
        this.$emit('main-toggle',id);
    }
  }
};
</script>
