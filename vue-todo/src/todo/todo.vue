<template>
    <div >
        <section class="real-app">
        <input 
            type="text" 
            class="add-input"
            autofocus="autofocus"
            placeholder="接下去要做什么?"
            @keyup.enter="addTodo"
        >
        <Item 
            :todo="todo"
            v-for="todo in todoFilterList"
            :key="todo.id"
            @del="deleteTodo"
            ></Item>
        <tabs :filter="filter" 
        @toggle="toggle"
        @delCompeleted="delCompeleted"
        :todos="todos"></tabs>
    </section>
    </div>
</template>

<script>
import dataList from "./data.vue"
import Item from "./items.vue"
import Tabs from "./tabs.vue";
let id = 0
export default {
    data() {
        return {
            todos:dataList,
            filter:'all'
        }
    },
    components:{
        Item,Tabs
    },
    computed:{
        
        todoFilterList(){
            if(this.filter==='all'){
                return this.todos
            }
            const completed = this.filter === 'completed'
            return this.todos.filter(todo=>todo.completed=== completed)
        },
        

    },
    methods: {
        addTodo(e){
            this.todos.unshift({
                id:id++,
                content:e.target.value.trim(),
                completed: false

            })
            e.target.value=''
        },
        deleteTodo(id){
            this.todos.splice(this.todos.findIndex(todo=>todo.id===id),1)
        },
       toggle(state){
            this.filter = state
        },
        delCompeleted(){
            this.todos=this.todos.filter(todo=>!todo.completed)
        }
    }
}
</script>
<style lang="stylus" scoped>
.real-app
    width 600px
    margin 0 auto
    box-shadow 0 0 5px #666
   

.add-input

    position relative
    margin 0
    width 100%
    font-size 24px
    font-family inherit 
    line-height 1.4em
    border none
    outline none 
    color inherit 
    box-sizing border-box
    font-smoothing antialiased
    padding 16px 16px 16px 36px
    border none
    border-radius 5px 5px 0px 0px
    box-shadow inset 0 -2px 1px rgba(0, 0, 0, 0.03)
</style>
