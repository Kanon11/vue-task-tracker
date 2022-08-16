<template>
  <header>
  <h1>{{title}}</h1>
  <button-component :color="showAddTask?'red':'green'" :text="showAddTask?'cancle':'Add Task'" @togglebutton="onTogglebutton()"></button-component>
  </header>
</template>

<script>
import ButtonComponent from "./Button.vue";
export default {
    components:{
        ButtonComponent
    },
  name: "HeaderComponent",
  props:{
    title:String,
    showAddTask:Boolean
  },
  methods:{
    onTogglebutton(){
        this.$emit("main-toggle");
    }
  },
  emits:['main-toggle']
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>