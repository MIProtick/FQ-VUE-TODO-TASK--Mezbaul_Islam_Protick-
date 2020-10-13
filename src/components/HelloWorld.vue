<template>
  <div class="container">
    <h1>{{ todo.title }}</h1>
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



</style>
