<template>
  <div class="taskList">
    <h1>Task List</h1>
    <div class="taskInput">
      <input type="text" v-model="task" placeholder="Añadir Tarea">
      <button @click="addTask" :disabled="task ==''">Agregar Task</button>
    </div>
    <div class="taskEditInput" v-show="visibilidad">
      <input type="text" placeholder="Editar Nombre" v-model="taskEdited">
      <button class="taskRemove" @click="edit" :disabled="taskEdited ==''">Editar Task</button>
    </div>
    <div v-for="(task, index) in tasks" :key="task" class="listado">
      <p class="taskIndex">{{index+1}}</p>
      <p class="taskName">{{task}}</p>
      <p  class="taskEdit"> <button @click="inputToggle(index)"> &#9997;</button></p>
      <button class="taskRemove" @click="removeTask(index)">&#10060;</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'taskList',
  data:function(){
    return{
      tasks:[],
      task:'',
      taskEdited:'',
      visibilidad: false,
      indexSelected: '',
    }
  },
  methods:{
    addTask(){
      this.tasks.push(this.task)
      this.task = ''
    },
    inputToggle(i){
      this.indexSelected = i
      this.visibilidad = true
    },
    removeTask(i){
      this.indexSelected = i
      this.tasks.splice(this.indexSelected, 1)
      this.indexSelected = ''
    }, 
    edit(){
      this.tasks.splice(this.indexSelected, 1, this.taskEdited)
      this.visibilidad = false
      this.indexSelected = ''
      this.taskEdited = ''
    }
  }
}
</script>

<style>
  .taskList{
    text-align: center;
    margin: auto;
  }
  .listado{
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 1rem;
    border: 1px solid gainsboro;
    margin: .5rem auto;
    padding: 0 1rem;
    width: 50%;
  }
  .taskIndex{
    padding-right: .5rem;
    border-right: 1px solid gainsboro;
  }
  .taskName{
    flex-grow: 2;
    text-align: left;
  }
  .taskInput *, .taskEditInput *{
    margin: .5rem;
  }
</style>