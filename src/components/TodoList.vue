<script setup>
import { computed, ref } from 'vue';

    const inputData = ref("");
    const todoList = ref([{text:'Item 1', completed: false}, {text:'Item 2', completed: true}, {text:'Item 3', completed: false}]);
    const editingTask = ref(-1);
    const filterTask = ref('All');

    const handleClick = () =>{
        if(inputData.value != "")
        {
          todoList.value = [...todoList.value, {text: inputData.value, completed: false}];
          const completedTask = todoList.value.filter((task) => task.completed);
          const activeTask = todoList.value.filter((task) => !task.completed);
          todoList.value = [...activeTask, ...completedTask];
          inputData.value = "";
        }
    }

    const deleteTask = (id) =>{
        todoList.value.splice(id, 1);
    }

    const editTask = (id) =>{
        editingTask.value = id;
    }

    const saveEditedTask = () =>{
        editingTask.value = -1;
    }

    const handleFilter = (event) =>{
        filterTask.value = event.target.value;
    }

    const filteredTasks = computed(() => {
    if (filterTask.value === 'completed') {
      return todoList.value.filter((task) => task.completed);
    } 
    else if (filterTask.value === 'active') {
      return todoList.value.filter((task) => !task.completed);
    } 
    else {
      return todoList.value;
    }
  });
</script>



<template>
    <div class="list" > 
        <h3>2023 Task List</h3>
        <div class="listInput">
            <div class="inputInput"><input class="input" type="text" placeholder="Add your Task here....." v-model="inputData" @keydown.enter="handleClick"/></div>
            <div class="inputButton"><input class="button" type="button" value="Add Task"  @click="handleClick"/></div>
        </div>
        <div class="listTasks">
            <div class="filter">
                <span class="filterCount">Tasks</span>
                <span class="filterSelect">
                    <select name="Filter" @change="handleFilter">
                      <option value="all">All</option>
                      <option value="active">Active</option>
                      <option value="completed">Completed</option>
                    </select>
                </span>
            </div>
            <div class="task" v-for="(item, index) in filteredTasks" :key="index" :class="{ 'completed-task': item.completed }" >
                <input type="checkbox" class="custom-checkbox" v-model="item.completed">
                <span v-if="index !== editingTask" class="taskInput">{{ item.text }}</span>
                <input v-else  v-model="todoList[index].text" class="taskInput" @blur="saveEditedTask" @keyup.enter="saveEditedTask">
                <span class="taskSelect">
                    <span class="delete" @click="deleteTask(index)">Delete</span>
                    <span class="edit" @click="editTask(index)">Edit</span>
                </span>
            </div>
        </div>
    </div>
</template>



<style>

    ::placeholder {
      color: #e8e0e0; /* Text color */
      font-style: italic; /* Italicize the text */
    }

    h3{
        font-weight: bolder;
        font-size:x-large;
        color:  rgb(0, 128, 255);
        height: 40px;
        text-decoration: underline;
    }

    .list{
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: #ffff;
        border-radius: 17px;
        width: 37%;
        height: 90%;
        padding: 20px 10px;
        gap: 20px;
    }
    .listInput{
        width: 100%;
        height: 9%;
        border: 1px solid transparent; 
        display: flex;
        align-items: center;
        justify-content: center;
        border: none;
        gap: 10px;
        
    }

    .inputInput{
        display: flex;
        align-items: center;
        justify-content: center;
        flex: 5;
        width: 80%;
        height: 90%;
        border: 1px solid rgb(47, 158, 255);
        border-radius: 5px;
    }
    .input{
        width: 95%;
        height: 95%;
        font-size: larger;
        outline: none;
        border: none;
        color: rgb(54, 54, 164);
    }
    .inputButton{
        flex: 1;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 94%;
        border-radius: 10px;
        border: 1px solid rgb(47, 158, 255);
        cursor: pointer;
    }
    .button{
        width: 100%;
        height: 100%;
        border: none;
        border-radius: 10px;
        cursor: pointer;
        color: #e0eaec;
        background-color: rgb(0, 128, 255);
    }

    .listTasks{
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 100%;
        height: 94%;
        overflow-y: scroll;
        overflow-x: hidden;
        gap: 10px;
    }
    .listTasks::-webkit-scrollbar {
      width: 4px; /* Scrollbar width */
    }

    .listTasks::-webkit-scrollbar-thumb {
      background: #858380; /* Thumb color */
      border-radius: 10px; /* Rounded corners */
    }

    .listTasks::-webkit-scrollbar-thumb:hover {
      background: #035166; /* Thumb color on hover */
    }
    
    .filter{
        display: flex;
        width: 95%;
        justify-content: space-between;
    }
    .filterSelect{
        background-color: rgb(0, 128, 255);
        width: 20%;
        border-radius: 7px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    select{
        height: 91%;
        width: 91%;
        border: none;
        outline: none;
        background-color: transparent;
        cursor: pointer;
        color: #ffff;
        font-weight: bold;
    }
    select option{
        display: flex;
        color: rgb(0, 128, 255);
        border-radius: 17px;
        font-weight: bold;
    }

    .task{
        display: flex;
        align-items: center;
        background-color: rgb(109, 232, 193);
        padding: 0px 15px;
        border-radius: 10px;
        width: 95%;
        height: 12%;
        overflow: hidden;
    }
    .task:hover .taskSelect {
       display: flex;
    }
    .custom-checkbox{
        position: relative;
        padding-left: 30px;
        cursor: pointer;
    }

    .taskInput{
        overflow: hidden;
        overflow-wrap: break-word;
        display: flex;
        align-items: center;
        width: 80%;
        height: 70%;
        border: none;
        outline: none;
        font-size: large;
    }
    .custom-checkbox:checked + .taskInput{
        text-decoration: line-through;
        color: red;
    }
    .completed-task :not(.custom-checkbox){
        opacity: 0.4;
    }


    .taskSelect{
        display: none;
    }
    .task:hover .taskSelect{
        display: flex;
        width: 25%;
        height: 90%;
        padding: 10px;
        gap: 10px;
        justify-content: center;
        align-items: center;
        justify-content: space-between;
    }
    .delete{
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        background-color: rgb(255, 0, 55);
        color: #ffff;
        font-size: medium;
        height: 60%;
        width: 95%;
        border-radius: 7px;

    }
    .edit{
        display: flex;
        cursor: pointer;
        justify-content: center;
        align-items: center;
        background-color: rgb(0, 140, 255);
        color: #ffff;
        font-size: medium;
        height: 60%;
        width: 95%;
        border-radius: 7px;
    }
</style>
