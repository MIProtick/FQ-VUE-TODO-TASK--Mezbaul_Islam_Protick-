<template>
  <div class="container" id="cntnr">
    <div class="todo_head">Tasks To-Do</div>
    <InsertTodo @addtd="addtodo($event)" />
    <div v-for="(todo, index) in todolist" :key="todo.id" class="tasklist">
      <Listing :todo="todo" :index="index" @rmtodo="removetodo($event)" @shwtodo="showtodo($event)" />
    </div>
  </div>
  <div>
    <Modal id="modal"  @closemdl="closemodal()" :todo="todolist[zoom_indx]" />
  </div>
  
  
</template>

<script>
import InsertTodo from './components/InsertTodo.vue'
import Listing from './components/Listing.vue'
import Modal from './components/Modal.vue'
import { ref } from 'vue'


export default {
  name: 'App',
  mounted(){
    if(localStorage.todolist){
      this.todolist = JSON.parse(localStorage.todolist);
    }
  },
  watch:{
    todolist:{
      handler(newTodolist){
        localStorage.todolist = JSON.stringify(newTodolist);
      },
      deep:true
    }
  },
  setup(){
    const todolist = ref([]);
    var p = []
    var zoom_indx = ref(0);

    if(localStorage.todolist){
      todolist.value = JSON.parse(localStorage.todolist);
      p = todolist.value.map((e)=>e)
    }

    function addtodo(todo){
      todolist.value.push({
        id: todolist.value.length,
        title: todo.title,
        desc: todo.description,
        duedate: todo.duedate,
      });
      p = todolist.value.sort((a,b)=>{
          return a.duedate>b.duedate
      });
      todolist.value = p.map((e)=>e);
    }

    function removetodo(index){
      todolist.value.splice(index, 1);
      delete p[index]
    }

    function closemodal(){
      document.getElementById('modal').style.display = 'none';
      document.getElementById('cntnr').style.filter = "blur(0px)"

    }

    function showtodo(index){
      if(p[index]){
        zoom_indx.value = index;
        document.getElementById('modal').style.display = 'block';
        document.getElementById('cntnr').style.filter = "blur(5px)"
      }
      else{
        p.splice(index, 1);
      }
    }

    return{
      todolist,
      zoom_indx,
      addtodo,
      removetodo,
      InsertTodo,
      showtodo,
      closemodal,
      Listing,
      Modal,
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

#modal{
  display: none;
}
</style>
