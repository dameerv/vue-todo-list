<template>
    <div>
        <h2>Todos</h2>
        <router-link to="/">Home</router-link>
        <AddTodo
                @add-todo="addTodo"
        />
        <select v-model="filter">
            <option value="all" selected>All</option>
            <option value="completed">Completed</option>
            <option value="not-completed">Not Completed</option>
        </select>
        <hr>
        <Loader v-if="loading" />
        <Todolist
                v-else-if="filteredToDos.length"
                v-bind:todos="filteredToDos"
                @remove-todo="removeTodo"
        />
        <p v-else>No todos</p>
    </div>
</template>

<script>
    import Todolist from "@/components/Todolist";
    import AddTodo from "@/components/AddTodo";
    import Loader from "@/components/Loader";

    export default {
        data(){
            return {
                todos:[],
                loading: true,
                filter:'All'
            }
        },
        mounted() {
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=4')
                .then(response => response.json())
                .then(json => {
                    setTimeout(() => {
                        this.todos = json
                        this.loading = false
                    }, 1000
                )
                })
        },
        // watch: {
        //     filter(value){
        //          console.log(value)
        //     }
        // },
        computed:{
            filteredToDos(){
                 if(this.filter === 'All'){
                     return this.todos
                 }
                 if(this.filter === 'completed'){
                     return this.todos.filter(t => t.completed)
                 }
                if(this.filter === 'not-completed'){
                    return this.todos.filter(t => !t.completed)
                }

            }
        },
        methods: {
            removeTodo(id){
                this.todos = this.todos.filter(t => t.id !== id)
            },
            addTodo(todo){
                this.todos.push(todo)
            }
        },
        components: {
            Todolist, AddTodo, Loader
        },
        name: 'Todos'
    }
</script>
<style scoped>

</style>