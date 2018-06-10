<template>
    <section class="real-app">
        <input 
        type="text"
        class="add-input"
        autofocus="autofocus"
        placeholder="接下来做什么"
        @keyup.enter="addTodo"
        >
        <Item 
        :todo="todo"
        v-for="todo in filteredTodos"
        :key="todo.id"
        @del="deleteTodo"
        ></Item>   
        <Tabs 
        :filter="filter" 
        :todos="todos"
        @toggle="toggleFilter"
        @clearAll="clearAllCompleted"
        ></Tabs>
    </section>   
</template>
<script>
import Item from './item.vue'
import Tabs from './tabs.vue'
import '../assets/styles/todo.styl'
let id = 0
export default {
    data() {
        return {
            todos:[],
            filter:"all"
        }
    },
  components: {
      Item,
      Tabs
  },
  computed:{
      filteredTodos(){
          if (this.filter === 'all'){
              return this.todos
          }
          const completed = this.filter === 'completed'
          return this.todos.filter(todo => completed ===todo.completed)
      },

  },
  methods: {
      addTodo(e){
         if(e.target.value==''){
             alert("你什么都没有添加!")
         }
         else{
             this.todos.unshift({
              id:id++,
              content: e.target.value.trim(),
              completed:false
          }),
          e.target.value =''
         }
          
      },
     deleteTodo(id){
        //  console.log(todo => todo.id ===id);
         this.todos.splice(this.todos.findIndex(todo => todo.id ===id),1)
     },
     toggleFilter(state){
         this.filter =state
     },
     clearAllCompleted(){
         this.todos = this.todos.filter(todo => !todo.completed)
         
     }
  },
}
</script>


