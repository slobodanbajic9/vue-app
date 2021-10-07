<template>
  <div class="home">
    <img alt="Todo logo" src="../assets/todo.png">
    <h3>You have {{ todosCount }} Todos!</h3>
    <div>
      <input 
      v-model="data.newTodoName"
      @keyup.enter="addTodo"
      placeholder="Add a Todo"
      type="text"
      >
    </div>
    <div>
      <ul>
        <li v-for="(todo, index) in data.todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="deleteTodo(index)">X</button>
        </li>
      </ul>
    </div>
    
  </div>
</template>

<script>
import { computed, reactive, ref } from '@vue/reactivity'
import { watch } from '@vue/runtime-core'


export default {
  setup() {

    let data = reactive({
      newTodoName: '',
      todos: []
    })
    const swearWords = ['fuck', 'fart', 'ass']

    let todosCount = computed(()=> {
      return data.todos.length
    })

    function addTodo () {
      let newTodo = {
        id: Date.now,
        name: data.newTodoName
      }
      data.todos.push(newTodo)
      data.newTodoName = ''
    }

    function deleteTodo(index) {
      data.todos.splice(index, 1)
    }

    watch(data, (newValue)=>{
      if(swearWords.includes(newValue.newTodoName.toLowerCase())) {
        data.newTodoName = ''
        alert('You cannot use words like ' + newValue.newTodoName + '..')
      }
    })



    return {
      data,

      todosCount,

      addTodo,
      deleteTodo,
    }
  }
}
</script>

<style>
ul {
  list-style: none;
  padding: 0;
  width: 200px;
  margin: 20px auto 0;
}
input {
  padding: 30px;
  text-align: center;
  font-size: 23px;
}

li {
  border-bottom: 1px solid #ccc;
  display: flex;
  margin-bottom: 10px;
}
li span {
  flex-grow: 1;
  padding: 10px;
  font-size: 20px;
}
li button {
  height: 30px;
  width: 30px;
  font-size: 20px;
  background: #42b983;
  color: #000;
  border-radius: 5px;
}
li button:hover {
  background: #ccc;
  color: #000;
}
</style>
