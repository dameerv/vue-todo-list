<template>
    <form action="" @submit.prevent="onSubmit">
        <input type="text" v-model="title">
        <button>Create</button>
    </form>
</template>

<script>
    export default {
        data(){
            return {
                title: ''
            }
        },
        methods:{
            onSubmit(){
                if(this.title.trim()){
                    const newTodo = {
                        id: Date.now(),
                        title: this.title,
                        completed: false
                    }

                    this.$emit('add-todo', newTodo)
                    this.title = ''
                }
            }
        },
        name: "AddTodo"
    }
</script>

<style scoped>
    form{
        display: flex;
    }
    input{
        width: 70%;
    }
</style>