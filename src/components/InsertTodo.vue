<template>
    <!-- <form @submit.prevent="addTodo"> -->
    <form >
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
        <div v-if="msg.state" class="errmsg">{{ msg.val }}</div>
        <button type="submit" @click.prevent="send(addTodo())">Add the task</button>
    </form>

</template>

<script>
import { ref } from 'vue'
// import emitter from '../eventbus'


export default {
  name: 'InsertTodo',
  props: {
  },
  methods: {
    send(todo){
      this.$emit('addtd',todo);
    }
  },

  setup(){
    const title = ref('');
    const description = ref('');
    const duedate = ref(new Date());
    var msg = ref({state:false, val:""});

    function addTodo(){
      if (typeof(duedate.value) != "string" || duedate.value == "" || title.value == "" || description.value == "" ) {
          msg.value = {state:true, val:"Incomplete Submision. Please Complete First"};
      } else {
          let prevdate = new Date();
          prevdate = prevdate.getFullYear()+'-'+(prevdate.getMonth()+1)+'-'+(prevdate.getDate()-1);
          if (new Date(duedate.value).valueOf() <= new Date(prevdate).valueOf()) {
              msg.value = {state:true, val:"Date can't be previous."};
          } else {
              msg.value = {state:false, val:""};
              var p = {title: title.value, description: description.value, duedate: duedate.value, }
              title.value = "";
              description.value = "";
              duedate.value = "";
              
          }
      }
      return p;
    }

    return{
      title,
      description,
      duedate,
      msg,
      addTodo,
    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

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



.form_section{
  display: flex;
  justify-content: space-evenly;
  width: 100%;
}

.form_part{
  display: inline;
  padding: 0 5px;
}

.errmsg{
  margin: 10px auto 0 auto;
  color: indianred;
  font-style: italic;
  font-size: 12px;
}

#todo_desc{
  width: 40%;
}

</style>
