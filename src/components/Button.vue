<template>
    <button class="btn" v-bind:style="{background:color}" v-on:click="click()">{{text}}</button>
</template>
<script>
export default{
    name:"ButtonComponent",
    props:{
        text:String,
        color:String
    },
    methods:{
        click(){
            this.$emit("togglebutton");
        }
    }
}
</script>