<template>
  <div class="">
    <div class="todo_card">
      <div class="ttl_show">
        <h6>Title</h6>
        <h4>{{ todo.title }}</h4>
        <div> Due: {{ todo.duedate }}</div>
      </div>
      <div class="description_show">
        <h6>Description</h6>
        <div>{{ todo.desc }}</div>
        <button class="delete">Delete</button>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    todo: Object,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

@import url('https://fonts.googleapis.com/css?family=Muli&display=swap');

.todo_card {
	background-color: #fff;
	border-radius: 10px;
	box-shadow: 0 0px 10px 5px rgba(0, 0, 0, 0.2);
	display: flex;
	max-width: 100%;
	margin: 20px;
	overflow: hidden;
	width: inherit;
}

.todo_card h6 {
	opacity: 0.6;
	margin: 0;
	letter-spacing: 1px;
	text-transform: uppercase;
}

.todo_card h4 {
	letter-spacing: 1px;
	margin: 5px 0;
  text-align: center;
}

.ttl_show {
	background-color: #2A265F;
	color: #fff;
	padding: 10px;
	width: 30%;
	max-height: 200px;
}

.ttl_show div{
  opacity: 0.7;
  font-size: 13px;
  padding: 10px 0 0 0;
}


.description_show {
	padding: 30px;
	position: relative;
	width: 70%;
}

.description_show h6 {
	opacity: 0.5;
  margin-bottom: 5px;
}

.description_show div{
  font-size: 15px;
  overflow: hidden;
  padding-right: 50px;
  text-align: justify;
}

.delete {
	background-color: #2A265F;
	border: 0;
	border-radius: 15px;
	box-shadow: 1px 1px 7px 3px rgba(0, 0, 0, 0.25);
	color: #fff;
	font-size: 10px;
	padding: 8px 16px ;
	position: absolute;
	bottom: 2%;
	right: 15px;
}

</style>
