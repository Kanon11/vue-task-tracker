<template>
  <div>
    <h1>{{ data }}</h1>
    <h1>{{ msg }}</h1>
    <button >click here</button>
  </div>
</template>
<script>
export default {
  name: "HomeComponent",
  props: {
    data: String,
    msg: String,
  },
  methods: {
    hello() {
      alert("hello function called");
    },
  },
};
</script>