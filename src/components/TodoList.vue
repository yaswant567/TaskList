<script setup>
import { ref } from 'vue';

    const inputData = ref("");
    const todoList = ref(['Item 1', 'Item 2', 'Item 3']);

    const handleClick = () =>{
        todoList.value = [...todoList.value, inputData.value];
        inputData.value = "";
    }

    const deleteTask = (id) =>{
        
    }
</script>

<template>
    <div class="list" > 
        <div class="listInput">
            <input type="text" v-model="inputData"/>
            <input class="inputButton" type="button" @click="handleClick"/>
        </div>
        <div class="listTasks">
            <div class="task" v-for="(item, index) in todoList" :key="index">
                <span>{{ item }}</span>
                <span class="taskSelect">
                    <span class="delete" @click="deleteTask(index)">Delete</span>
                    <span class="edit" @click="editTask(index)">Edit</span>
                </span>
            </div>
        </div>
    </div>
</template>

<style>
    .list{
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: #ffff;
        border-radius: 17px;
        width: 40%;
        height: 90%;
        padding: 20px 10px;
        gap: 30px;
    }
    .listInput{
        width: 100%;
        height: 6%;
        border: 1px solid transparent; 
        display: flex;
        align-items: center;
        justify-content: center;
        border: none;
        border-bottom: 1px solid rgb(2, 71, 7);
    }
    .inputButton{
        cursor: pointer;
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
    
    .task{
        display: flex;
        align-items: center;
        justify-content: space-between;
        background-color: rgb(109, 232, 193);
        padding: 0px 15px;
        border-radius: 10px;
        width: 95%;
        height: 12%;
    }
    .taskSelect{
        display: flex;
        width: 20%;
        height: 60%;
        padding: 10px;
        gap: 10px;
        justify-content: center;
        align-items: center;
        justify-content: space-between;
    }
    .delete{
        cursor: pointer;
    }
    .edit{
        cursor: pointer;
    }
</style>
