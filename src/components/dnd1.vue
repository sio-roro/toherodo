<template>
  <div class="main">
    <h1 v-if=drag class="header">changing</h1>
    <h1 v-else class="header">{{header}}</h1>
    <div class="indicator" v-if=drag :class="{ inMove: drag||coution }"></div>
    <div class="indicator" v-else  :class="{ inMove: drag||coution }"></div>
    <div class="input-area">
      <div class="text-input" >
        <input type="text" v-model="inputText" id="input1" placeholder="Type what to do today in here!">
        <label for="input1">Todo</label>    
      </div>
      <button v-on:click="addTodo" class="btn-flat">Add it</button> 
    </div> 
     
    <div class="todo-area">
      <div class="harf-content">
          <draggable class="itemA " v-model="todos" group="myGroup" @start="drag=true" @end="drag=false"  :options="options"   @add="onAdd">
          <div  v-for="(todo, index) in todos" :key="todo.id" >
              <div class="item" >
                <i class="fas fa-bars"></i>
                <input type="checkbox"  name="checkbox" v-bind:id="'box-1'+index" v-model="todo.isDone" v-on:change="checked(todo)" >
                  <label v-bind:for="'box-1'+index" v-if=todo.isDone class="done-item"> {{todo.item}}</label>
                  <label v-bind:for="'box-1'+index" v-else> {{todo.item}}</label>
                  <div v-on:click="deleteTodo(index)" class="del-btn"><i class="fas fa-times"></i></div>
              </div>
          </div>
          </draggable>
          <h3 class="countA">{{todos.length}}</h3>
      </div>
      <div class="harf-content">
        <draggable  class="itemB " v-model="itemsB" group="myGroup" @start="drag=true" @end="drag=false"  :options="options"   @add="onAdd">
            <div v-for="(todo, index) in itemsB" :key="todo.id"  >
              <div class="item">
                <i class="fas fa-bars"></i>
                <input type="checkbox" v-bind:id="'box-2'+index" v-model="todo.isDone" v-on:change="checked(todo)" >
                <label v-if=todo.isDone class="done-item" v-bind:for="'box-2'+index" > {{todo.item}}</label>
                <label v-else v-bind:for="'box-2'+index"> {{todo.item}}</label>
                <div v-on:click="deleteTodoB(index)"><i class="fas fa-times"></i></div>
              </div>
            </div>
          </draggable>
          <h3 class="countB">{{itemsB.length}}</h3>
      </div>
          
    </div>
  </div>
</template>

<script>
  import draggable from 'vuedraggable'

  export default {
      name: "dnd",
      components: { draggable },
      data () {
          return {
              options: {
                  group: "myGroup",
                  animation: 200
              },
              todos: [],
              itemsB: [],
              header:"HERO",
              inputText:'',
              drag: false,
              coution:false
              
          }
      },
      
      methods:{
          addTodo:function(){
            var todo={
          item:this.inputText,
          isDone:false
        }
       
        if(!this.inputText==''){
          this.todos.push(todo)
          localStorage.Todos=JSON.stringify(this.todos)
          this.inputText=""
          this.header="Registered"
          this.coution=false
        }else{
          this.header="Edit me"
          this.coution=true
        }

        },
        deleteTodo:function(index){
        this.todos.splice(index,1)
        localStorage["Todos"]= JSON.stringify(this.todos);
        this.header="Deleted"
        },
        deleteTodoB:function(index){
        this.itemsB.splice(index,1)
        localStorage["TodosB"]= JSON.stringify(this.itemsB);
        this.header="Deleted"
        },
        checked:function(todo){
        localStorage.Todos=JSON.stringify(this.todos)
        localStorage.TodosB=JSON.stringify(this.itemsB)
        if (todo.isDone){
          this.header="Done!!!"
          this.coution=false
        }else{
          this.header="Removed"
          this.coution=false
        }
        
        },
        onAdd:function() {
          
            localStorage.Todos=JSON.stringify(this.todos)
            localStorage.TodosB=JSON.stringify(this.itemsB)
            this.header="HERO"
            this.coution=false

        }
        

        
        


        
      },
      created(){
        this.todos = JSON.parse(localStorage["Todos"]);
        this.itemsB = JSON.parse(localStorage["TodosB"]);
      }
  }
  
</script>

<style scoped>
body{
  background-color: #c0c0c0;
}
.main{
  
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  overflow: scroll;
}
.header{
  color:#ddd;
  font-size: 50px;
}
  .item {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: row;
    margin: 10px;
    padding: 10px;
    border: 1px solid #7f7f7f;
    border-radius: 10px;
    background-color: #dcdcdc;

  }
  .item:hover {
    cursor: grab;
    background-color:#ffffff;
    transition: all 0.3s;
  }
  .item:active {
    cursor: grabbing;
     background-color:#008b8b;
     border:1px solid #008b8b;
    
  }
  .item:active .fa-times{
    color: #008b8b;
    transition: all 0.3s;
  }
  .fa-times{
    color: #dcdcdc;
    font-size:25px;
    padding-left:7px;
  }
  .fa-times:hover{
     color:red;
     transition: all 0.3s;
  }
  .del-btn{
    display: flex;
    align-items: center;
    justify-content: center;
  }
   .checkbox{
    width: 20px;
    height:20px;
  }
  .caution{
    color: #ff8c00;
  }
  .done-item{
    text-decoration: line-through;
    opacity: 0.3;
  }
  .todo-area{
    height: 100%;
    width: 80%;
    display: flex;
    align-items: flex-start;
    justify-content: flex-start;
    flex-direction: row;
  }
  .itemA{
    
    width: 100%;
    min-height: 300px;
    border-top:10px solid #ff8c00;
    border-bottom: 10px solid #ff8c00;
    padding: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
  }
  .itemB{
    min-height: 300px;
    width: 100%;
     border-bottom: 10px solid#008b8b;
    border-top:10px solid #008b8b;
    padding: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
  }
  .inMove {
  background: #ff8c00 !important;
}
.indicator {
  margin: auto;
  width: 300px;
  height: 30px;
  border-radius: 3px;
  background: #42b983;
}
.areaA{
  height: 100px;
  width: 100%;
  background-color: aqua;
}
.areaB{
  height: 100px;
  width: 100%;
  background-color:green;
}

 @import url(https://fonts.googleapis.com/css?family=Open+Sans);

/*Page styles*/
html { height: 100%; 
background: #484848;}

body {
  height: 100%;
  margin: 0;
  background: #363636;
  display: -webkit-flex;
  display: flex;
  align-items: center;
}

.boxes {
  
  padding: 50px;
  background: #484848;
}

/*Checkboxes styles*/
input[type="checkbox"] { 
  display: none; 
  }

input[type="checkbox"] + label {
  display: block;
  position: relative;
  padding-left: 35px;
  
  font: 14px/20px 'Open Sans', Arial, sans-serif;
  color: black;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
}

input[type="checkbox"] + label:last-child { 
  margin-bottom: 0; 
  }

input[type="checkbox"] + label:before {
  content: '';
  display: block;
  width: 20px;
  height: 20px;
  border: 2px solid #008b8b;
  position: absolute;
  left: 0;
  top: -2px;
  opacity: 0.8;
  -webkit-transition: all .12s, border-color .08s;
  transition: all .12s, border-color .08s;
}

input[type="checkbox"]:checked + label:before {
  width: 10px;
  top: -5px;
  left: 5px;
  border-radius: 0;
  opacity: 1;
  border-top-color: transparent;
  border-left-color: transparent;
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
}
@import  url(https://fonts.googleapis.com/css?family=Montserrat);

body{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: Montserrat;
  background: #313E50;
}

.text-input{
  
  position: relative;
  margin-top: 50px;
}
  .text-input input[type="text"]{
    display: inline-block;
    width: 500px;
    height: 40px;
    box-sizing: border-box;
    outline: none;
    border: 1px solid lightgray;
    border-radius: 3px 0 0 3px;
    padding: 10px 10px 10px 100px;
    transition: all 0.1s ease-out;
  }
  
  .text-input input[type="text"] + label{
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    height: 40px;
    line-height: 40px;
    color: white;
    border-radius: 3px 0 0 3px;
    padding: 0 20px;
    background:#42b983;
    transform: translateZ(0) translateX(0);
    transition: all 0.3s ease-in;
    transition-delay: 0.2s;
  }
  
  .text-input input[type="text"]:focus + label{
    transform: translateY(-120%) translateX(0%);
    border-radius: 3px;
    transition: all 0.1s ease-out;
  }
  
  .text-input input[type="text"]:focus{
    padding: 10px;
    transition: all 0.3s ease-out;
    transition-delay: 0.2s;
  }
  .input-area{
    display: flex;
    align-items: flex-end;
    justify-content: center;
    flex-direction: row;
    margin-bottom: 40px;
  }
  button{
    padding: 20px;
    color: white;
    background-color:#42b983;
    font-family: Montserrat;
    height: 40px;
    border:0px solid #42b983;
    border-radius: 0 3px 3px 0;
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0.7;
  }
  button:hover{
    opacity: 1;
    background-color: #ff8c00;
    transition: all 0.3s;
    border:0px solid #42b983;
  }
  .fa-bars{
    font-size:20px;
    padding-right:7px;
    color:#008b8b;
  }
.harf-content{
  width:50%;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  flex-direction: column;
}
.countA{
  color: #ff8c00;
}
.countB{
  color:#008b8b;
}

  
</style>