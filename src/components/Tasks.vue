<template>
    <div :key="task.id" v-for="task in tasks">
        <!-- <console class="log">{{task}}</console> -->
        <EachTask 
            @toggle-reminder="$emit('toggle-reminder', task._id)"
            @delete-task="$emit('delete-task', task._id)"
            :task="task"/>
    </div>
</template>

<script>
import  EachTask from './Task.vue'
import { ENV } from '../config/config'


export default {
    name: "ListTask",
    props:{
        tasks: Array,
    },
    components:{
        EachTask
    },
    emits: ['delete-task', 'toggle-reminder','update-Task-List'],
    created(){
        console.log("url :",ENV.url)
        let url = `${ENV.url}task/`
        fetch(url, {
            method:'GET',
        }).then(res => res.json()).then(data => {
            if(data.success){
                console.log('data: ',data.data.tasks);
                this.$emit('updateTaskList', data.data.tasks)
                // this.tasks = data.data.tasks;
            }
        }).catch(error=>{
            console.log('error: ',error)
        })
    },
    mounted() {
        // alert('here we go')
        console.log(`the component is now mounted.`)
        let url = `${ENV.url}task/`
        fetch(url, {
            method:'GET',
        }).then(res => res.json()).then(data => {
            if(data.success){
                console.log('data: ',data.data.tasks);
                this.$emit('update:tasks', data.data.tasks)
                // this.tasks = data.data.tasks;
            }
        }).catch(error=>{
            console.log('error: ',error)
        })
    }
}
</script>
