<template>
    <div class="modal_bg">
      <div id="mymodal_box" class="modal_box">
          <div class="line-numbers"></div>
          <div class="modal-content">
          <div class="modal_1st">
              <div class="modal_id"><div>Id <br> {{ todo.id }} </div> </div>
              <div class = "modal_1st_2nd">
              <div class="modal_ttl"> {{ todo.title }} </div>
              <div class="modal_ttl">Due : {{ todo.duedate }} </div>
              </div>
          </div>
          <div class="modal_2nd">
            <div>Description: </div>
              <div> {{ todo.desc }} </div>
          </div>
          
          </div>
          <span class="close" @click="closemodal()" >&times;</span>
      </div>
    </div>
</template>

<script>
// import emitter from '../eventbus'

export default {
  name: 'Modal',
  emits:{
	'closemdl': null,
  },
  props: {
    todo: Object,
  },
  methods: {
    closemodal(){
      this.$emit('closemdl');
    },
  },
  setup(){

    window.onclick = function(event) {
      var modalbg = document.getElementsByClassName("modal_bg")[0];
      if (event.target == modalbg) {
        document.getElementById('modal').style.display = 'none';
        document.getElementById('cntnr').style.filter = "blur(0px)"
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.modal_box {
  display: flex;
  position: fixed; 
  left: 21%;
  top: 30%;
  width: 50%;
  min-width: 48%;
  padding: 20px 27px 20px 20px;
  border-radius: 0 15px;
  z-index: 1; 
  overflow: auto;
  background: linear-gradient(25deg, rgba(21,50,101,0.95) 0%, rgba(51,73,131,0.7) 40%, rgba(10,90,138,0.8) 100%);
}

/* Modal Content */
.modal-content {
  background-color: rgba(255,255,255, 0.8);
  margin: auto;
  padding: 20px;
  border-radius: 0 9px;
  box-shadow: 0px 0px 7px 4px rgba(0, 0, 0, 0.25);
  width: 100%;
}

.modal_1st{
  display: flex;
  font-family: Comic Sans MS;
  text-align: center;
  margin-bottom: 8px;
}
.modal_id{
  width: 80px;
  height: 80px;
  background: rgba(21,50,100,0.5);
  border-radius: 40px;
}
.modal_id div{
  margin: 20% 0;
}
.modal_1st_2nd{
  width: 73%;
  padding: 8px;
  display: flex;
flex-direction: column;
justify-content: space-between;
}
.modal_1st_2nd div:nth-child(1){
  flex-grow: 2;
  margin-bottom: 8px;
  font-size: 22px;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
}
.modal_1st_2nd div:nth-child(2){
  font-family: Roboto;
  opacity: 0.6;
}

.modal_2nd{
  max-height: 150px;
  min-height: 80px;
  overflow: hidden;
}
.modal_2nd div:nth-child(1){
  text-align: center;  
  color: rgba(21,50,101,0.5);
  font-family: "Comic Sans MS", "Comic Sans", cursive;
}
.modal_2nd div:nth-child(2){
  text-align: center;
  color: rgba(21,50,101,0.8);
  font-family: "Comic Sans MS", "Comic Sans", cursive;
}

.close {
  color: rgba(213,234,209,1);
  float: right;
  font-size: 28px;
  font-weight: bold;
  position: absolute;
  top: 2px;
  right: 8px;
}

.close:hover,
.close:focus {
  color: rgba(25,86,17,1);
  text-decoration: none;
  cursor: pointer;
}

.modal_bg{
  display: none;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  top: 0;
  position: fixed;
  left: 0;
  z-index: 1;
  background-color: rgba(227, 218, 184, 0.1);
}

</style>
