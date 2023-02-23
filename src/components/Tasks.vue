<template>
    <div :key="task.id" v-for="task in tasks">
        <!-- <console class="log">{{task}}</console> -->
        <EachTask 
            @toggle-reminder="$emit('toggle-reminder', task.id)"
            @delete-task="$emit('delete-task', task.id)"
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
    emits: ['delete-task', 'toggle-reminder'],
    created(){
        console.log("url :",ENV.url)
        let url = `${ENV.url}task/`
        fetch(url, {
            method:'GET',
        }).then(res => res.json()).then(data => {
            if(data.success){
                console.log('data: ',data);
            }
        }).catch(error=>{
            console.log('error: ',error)
        })
    }
}
</script>
