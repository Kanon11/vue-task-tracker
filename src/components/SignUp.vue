<template>
  <img class="logo" src="../assets/logo.png">
    <h1>Sign Up</h1>
    <div class="inputContainer">
    <input type="text" placeholder="Enter Name"><br>
    <input type="text" placeholder="Enter Email"><br>
    <input type="password" placeholder="Enter Password"><br>
    <button>Sign Up</button>
    </div>
</template>
<script>
export default {
    name:'SignUp'
}
</script>
<style scoped>
.logo{
    width: 100px;
}
.inputContainer input{
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid skyblue;
}
.inputContainer button{
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    background-color: skyblue;
    color: aliceblue;
}
</style>