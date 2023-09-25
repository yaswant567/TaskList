<script setup>
import { ref } from 'vue';

    const inputData = ref("");
    const todoList = ref([{text:'Item 1', completed: false}, {text:'Item 2', completed: false}, {text:'Item 3', completed: false}]);
    const editingTask = ref(-1);
    const filterTask = ref('All');

    const handleClick = () =>{
        todoList.value = [...todoList.value, {text: inputData.value, completed: false}];
        inputData.value = "";
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
</script>



<template>
    <div class="list" > 
        <div class="listInput">
            <div class="inputInput"><input class="input" type="text" v-model="inputData" @keydown.enter="handleClick"/></div>
            <div class="inputButton"><input class="button" type="button" value="Add Task"  @click="handleClick"/></div>
        </div>
        <div class="listTasks">
            <div class="task" v-for="(item, index) in todoList" :key="index">
                <span v-if="index !== editingTask">{{ item }}</span>
                <input v-else v-model="todoList[index]" type="text" @blur="saveEditedTask" @keyup.enter="saveEditedTask">
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
        height: 9%;
        border: 1px solid transparent; 
        display: flex;
        align-items: center;
        justify-content: center;
        border: none;
        
    }
    .inputInput{
        flex: 5;
        width: 90%;
        height: 90%;
        border: 1px solid rgb(47, 158, 255);
        border-radius: 10px;
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
