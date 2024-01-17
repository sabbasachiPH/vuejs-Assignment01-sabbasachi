<script setup>
import { reactive, ref } from 'vue'
import taskList from './taskList'


const assignmentTitle = "Assignment-01 [Module 01-05] ";
const tableTitle = "Task List";
let showAddTaskForm = ref(false);

let tasks = reactive(taskList);
let newTask = reactive({
  id: tasks.length + 1,
  name: '',
  time: 0,
  isDeleted: false,
})

function addNewTask() {
  showAddTaskForm.value = !showAddTaskForm.value;
}

function saveNewTask() {
  tasks.push(newTask);
  showAddTaskForm = !showAddTaskForm;

}

function deleteTask(id) {
  const itemPosition = tasks.findIndex(task => id === task.id);
  tasks.splice(itemPosition, 1);
}


</script>

<template >
  <div class="w-screen h-screen flex justify-center items-center mx-auto my-3 bg-slate-300" v-show="showAddTaskForm">
    <div>
      <form @submit.prevent="saveNewTask">
        <p>Task Title: {{ newTask.name }}</p>
        <input v-model.trim="newTask.name" placeholder="Enter Task Detail"
          class="border-black-600 m-2 p-2 bg-slate-200" />
        <p>Time Required: {{ newTask.time }}</p>
        <input v-model.trim="newTask.time" placeholder="0.00 seconds" class="border-black-600 m-2 p-2 bg-slate-200" />
        <p> <button type="submit" class="rounded bg-slate-500 p-2"> Save Task</button></p>
      </form>
    </div>
    <!-- <div class="container">
      Task ID: <input class="border-black-600 m-2 p-2 bg-slate-200" type="text" name="taskId " value="" /><br>
      Task Name: <input class="border-black-600 m-2 p-2 bg-slate-200" type="text" name="taskTitle " value="" /><br>
      Time Required: <input class="border-black-600 m-2 p-2 bg-slate-200" type="text" name="taskTime " value="" /><br>
      Task Status: <input class="border-black-600 m-2 p-2 bg-slate-200" type="text" name="taskStatus " value="" /><br>

    </div> -->

  </div>
  <div class="max-w-[80vw] mx-auto my-3 bg-slate-400 " v-show="!showAddTaskForm">
    <button @click="addNewTask()" class="rounded bg-blue-600 text-white p-2 m-1">
      <span v-text="showAddTaskForm ? 'Close Form' : 'Add Task'"></span>
    </button>

  </div>




  <table class="table-auto text-center min-w-[70vw] mx-auto ">
    <caption class="caption-top text-3xl bold bg-gray-400 text-center">
      {{ tableTitle }}
    </caption>

    <thead>
      <th>Task Id</th>
      <th>Task Title</th>
      <th>Time Required (in minutes) </th>
      <th>Actions</th>
    </thead>
    <tbody>
      <template v-for="(task, index) in tasks" v-bind:key={index}>
        <tr>
          <td>{{ task.id }}</td>
          <td class=" text-red-500">{{ task.name }}</td>
          <td>{{ task.time }}</td>
          <td><button @click=deleteTask(task.id) type="submit"
              class="rounded bg-stone-800 text-white p-2 m-1">Delete</button></td>
        </tr>

      </template>
    </tbody>
  </table>
</template>



<style scoped>
table,
th,
td {
  border: 1px solid black;
  color: rgb(111, 0, 255);
  text-align: center;
  border-collapse: collapse;

}
</style>
