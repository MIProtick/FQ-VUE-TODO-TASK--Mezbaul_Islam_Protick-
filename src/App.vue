<template>
  <div class="container">
    <div class="todo_head">Tasks To-Do</div>
    <InsertTodo @addtd="addtodo($event)" />
    <div v-for="(todo, index) in todolist" :key="todo.id" class="tasklist">
      <Listing :todo="todo" :index="index" @rmtodo="removetodo($event)" />
    </div>
  </div>
  
</template>

<script>
import InsertTodo from './components/InsertTodo.vue'
import Listing from './components/Listing.vue'
import { ref } from 'vue'


export default {
  name: 'App',
  setup(){
    const todolist = ref([]);

    function addtodo(todo){
      console.log('-->'+todo.title);
      todolist.value.push({
        id: todolist.value.length,
        title: todo.title,
        desc: todo.description,
        duedate: todo.duedate,
      });
      let p = todolist.value.sort((a,b)=>{
          return a.duedate>b.duedate
      });
      todolist.value = p.map((e)=>e);
    }

    function removetodo(ev){
      console.log('-->'+ev);
      todolist.value.splice(ev, 1);
    }

    return{
      todolist,
      addtodo,
      removetodo,
      InsertTodo,
      Listing,
    }
  },
};
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Sansita+Swashed&display=swap');

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container{
  width: 70%;
  margin: auto;
}

.todo_head{
  font-size: 30px;
  font-family:Sansita Swashed;
}
</style>
