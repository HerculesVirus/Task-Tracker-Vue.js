<template>
    <header>
        <h1>
            {{title}}
        </h1>
    <AddButton @toggle-add-task="$emit('toggle-add-task')"   :title="addShowTask ? 'Close' : text" :color="addShowTask ? 'red' : color"/>
    </header>

</template>

<script>
import AddButton from './Button.vue'


export default {
    name : 'HeaderFirst',
    props : {
        title : {
            type: String ,
            default: "Hello Wolrd"
        },
        addShowTask : Boolean
    },
    components: {
        AddButton ,
    },
    data() {
        return {
            count : 1,
            text: 'Add Task',
            color: 'green'
        }
    }
}
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>

