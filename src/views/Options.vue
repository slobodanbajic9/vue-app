<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/todo.png">
    <h3>You have {{ todosCount }} Todos!</h3>
    <div>
      <input 
      v-model="newTodoName"
      @keyup.enter="addTodo"
      placeholder="Add a Todo"
      type="text"
      >
    </div>
    <div>
      <ul>
        <li v-for="(todo, index) in todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="deleteTodo(index)">X</button>
        </li>
      </ul>
    </div>
    
  </div>
</template>

<script>


export default {
  data() {
    return {
      newTodoName: '',
      todos: [],
      swearWords: ['fuck', 'fart', 'ass']
    }
  },
  computed: {
    todosCount () {
      return this.todos.length
    }
  },
  methods: {
    addTodo () {
      let newTodo = {
        id: Date.now,
        name: this.newTodoName
      }
      this.todos.push(newTodo)
      this.newTodoName = ''
    },
    deleteTodo (index) {
      this.todos.splice(index, 1)
    }
  },
  watch: {
    newTodoName(newValue) {
      if(this.swearWords.includes(newValue.toLowerCase())) {
        this.newTodoName = ''
        alert('You cannot use words like ' + newValue + '..')
      }
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
