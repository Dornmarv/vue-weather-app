<template>
    <div class="header">
      <h1>{{ msg }}</h1>
    </div>
  </template>
  
  <script>
  export default {
    name: "HeaderItem",
    props: {
      msg: String,
    },
  };
  </script>
  
  <style scoped>
  .header {
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin-bottom: 10px;
  }
  </style>
  