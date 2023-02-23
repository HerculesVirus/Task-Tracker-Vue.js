<template>
    <button :style="{ background : color}" class="btn" @click="$emit('toggle-add-task')">
        {{title}}
    </button>
</template>

<script>


export default {
    name : "AddButton",
    props :{
        title : String,
        color: String
    },
    data(){
        return{
            count : 1,
        }
    },
    watch:{
        // whenever count changes, this function will run
        count(){
            console.log("count=watch : ",this.count)
        }
       
    },

    methods:{
        changeCount(){
            // console.log("count : ",this.count)
            this.count++;
        }
    }
}
</script>
