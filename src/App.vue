<template>
  <div class="container">
    <HeaderFirst @toggle-add-task="toggleAddATask"  title="Task Tracker" :addShowTask='addShowTask' />
    <div v-show="addShowTask">
      <AddTask @add-task="addTask" />
    </div>

    <ListTask   @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks"  @update-Task-List="updateTaskList" />
  </div>
</template>

<script>
import HeaderFirst from './components/Header.vue';
import ListTask from './components/Tasks.vue';
import AddTask from './components/AddTask.vue';
import { ENV } from './config/config';


export default {
  name: 'App',
  components: {
    HeaderFirst,
    ListTask,
    AddTask
  },
  data(){
    return {
      tasks : [],
      addShowTask: false
    }
  },
  methods:{
    toggleAddATask(){
      this.addShowTask = !this.addShowTask
    },
    addTask(task){
      let url = `${ENV.url}task/create`;
      fetch(url ,{
        method:'POST',
        headers:{
          'content-type': 'application/json',
        },
        body: JSON.stringify(task)
      }).then(res => res.json())
      .then(data =>{
        if(data){
          task = data.task
        }
      })
      .catch(error=>{
        console.log('error: ',error)
      })
      this.tasks = [...this.tasks , task]
    },
    updateTaskList(list){
      this.tasks = list
    },
    deleteTask(id){
      let url = `${ENV.url}task/${id}`;
      fetch(url ,{
        method:'DELETE'
      }).then(res => res.json())
      .then(data =>{
        console.log("response from delete Task API: ",data)
      })
      .catch(error=>{
        console.log('error: ',error)
      })

      this.tasks = this.tasks.filter( (task) => task._id !== id)
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task)=>
      task.id === id ? {...task , reminder: !task.reminder} : task )
    }
  },
  created(){
    this.tasks = [
      {
        id: 1 , 
        text : "Doctor Appointment",
        day : "March 1st at 2:30pm",
        reminder : true ,
      },
      {
        id: 2, 
        text : "Table Tennis Time",
        day : "March 2nd at 1:30pm",
        reminder : true ,
      },
      {
        id: 3, 
        text : "Other problems Time",
        day : "March 3rd at 1:30pm",
        reminder : false ,
      }
    ]
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
