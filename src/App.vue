<script>
  import TodoList from './components/TodoList.vue';
  export default {
    name: 'App',
    components: {
      TodoList, 
    },
  }
</script>

<template>
  <div class="App">
    <TodoList/>
  </div>
</template>

<style >
  #app{
     display: flex;
     text-align: center;
     align-items: center;
     justify-content: center;
     color: rgb(54, 54, 164);
     font-size: large;
     font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
     margin: 0p;
  }
  .App{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100vw;
    height: 100vh;
    box-sizing: border-box;
    background-color: rgb(156, 220, 245);
  }
</style>