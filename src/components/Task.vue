<template>
    <div @dblclick="$emit('toggle-reminder', task.id)"
     :class="[task.reminder ? 'reminder' : '','task']">
        <h3>
            {{task.title}}
            <i @click="$emit('delete-task', task._id)" class="fas fa-times"></i>
        </h3>
        <p>{{task.date}}</p>
    </div>

</template>

<script>


export default {
    name : "EachTask",
    props:{
       task : {
        type: Object
       } 
    }
}
</script>

<style scope>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 10px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>