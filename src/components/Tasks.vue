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


export default {
    name: "ListTask",
    props:{
        tasks: Array,
    },
    components:{
        EachTask
    },
    emits: ['delete-task', 'toggle-reminder'],
}
</script>
