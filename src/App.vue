<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <div class="container">
    <form @submit.prevent="addTodo">
        <div class="form_section">
          <div class="form_part" id="todo_ttl">
            <input type="text" name="todo_title" v-model="title" placeholder="Title">
          </div>

          <div class="form_part" id="todo_desc">
            <input type="text" name="todo_description" v-model="description" placeholder="Descriptions">
          </div>

          <div class="form_part">
            <input type="date" name="due" id="due" v-model="duedate" placeholder="Due Date">
          </div>
        </div>

      <button type="submit">Add the task</button>
    </form>

    <div v-for="todo in todolist" :key="todo.id" class="tasklist">
      <!-- <h3> {{ todo.title }} </h3> -->
      <HelloWorld :todo="todo" />
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import { ref } from 'vue'

export default {
  // name: 'App',
  // components: {
  //   HelloWorld
  // }

  setup(){
    const title = ref('');
    const description = ref('');
    const duedate = ref(new Date());
    var msg = ref('');
    const todolist = ref([]);

    function addTodo(){
      if (typeof(duedate.value) != "string" || duedate.value == "" || title.value == "" || description.value == "" ) {
        msg.value = "In complete Submision. Please Complete First";
        alert(msg.value);
      } else {
        msg.value = "";
        todolist.value.push({
          id: todolist.value.length,
          title: title.value,
          desc: description.value,
          duedate: duedate.value,
        });
        title.value = "";
        description.value = "";
        duedate.value = "";
      }
    }

    return{
      title,
      description,
      duedate,
      msg,
      todolist,
      addTodo,
      HelloWorld,
    }
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

form {
  padding: 15px 45px;
  margin: 0 auto;
}

button, input {
  border: 0;
  outline: 0;
  font-size: 16px;
  border-radius: 40px;
  padding: 12px;
  background-color: #EBECF0;
  text-shadow: 1px 1px 0 #FFF;
}

label {
  display: block;
  width: 100%;
  margin: 10px 0 10px 0;
}

input {
  box-shadow: inset 2px 2px 5px #BABECC, inset -5px -5px 10px #FFF;
  width: 100%;
  box-sizing: border-box;
  transition: all 0.2s ease-in-out;
  appearance: none;
  -webkit-appearance: none;
}
input:focus {
  box-shadow: inset 1px 1px 2px #BABECC, inset -1px -1px 2px #FFF;
}

button {
  color: #61677C;
  font-weight: bold;
  box-shadow: -5px -5px 20px #FFF, 5px 5px 20px #BABECC;
  transition: all 0.2s ease-in-out;
  cursor: pointer;
  font-weight: 600;
  margin: 10px 0;
}
button:hover {
  box-shadow: -2px -2px 5px #FFF, 2px 2px 5px #BABECC;
}
button:active {
  box-shadow: inset 1px 1px 2px #BABECC, inset -1px -1px 2px #FFF;
}

.container{
  width: 70%;
  margin: auto;
}

.form_section{
  display: flex;
  justify-content: space-evenly;
  width: 100%;
}

.form_part{
  display: inline;
  padding: 0 5px;
}

#todo_desc{
  width: 40%;
}

</style>
