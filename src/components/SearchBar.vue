<template>
    <div class="input">
      <input
        type="text"
        class="search-bar"
        placeholder="Search..."
        id="location"
      />
    </div>
  </template>
    
    <script>
  export default {
    name: "SearchBar",
  };
  </script>
    
    <style scoped>
  .input {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    font-weight: 500;
  }
  .search-bar {
    box-sizing: content-box;
    width: 100%;
    font-size: 133%;
    height: 30px;
    padding: 10px 20px;
    border-radius: 10px;
    outline: none;
    background-color: grey;
    color: #f2f0e9;
    text-align: left;
    border: 1px solid grey;
  }
  .search-bar::placeholder {
    color: #f2f0e9;
    opacity: 0.5;
  }
  </style>
    