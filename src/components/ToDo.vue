<template>
  <div>
    <div>
      <input type="text" v-model="newTodoText" :disabled="editMode">
      <button @click="addTodo">ADD</button>    
    </div>
    <div>
      <h1 v-if="showTodoLeft">There are {{ todos.length }} todo left</h1>
      <ol>
        <li v-for="(todo, index) in todos" :key="index">
          <div v-if="editMode && index === editIndex">          
            <input type="text" v-model="editTodoText">
            <button @click="updateTodo(index)">UPDATE</button>
          </div>          
          <div v-else>
            <p>{{ modifiedTodos[index] }}</p>
            <button @click="editTodo(index)">EDIT</button>
          </div>
          <button @click="deleteTodo(index)">DELETE</button>
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
  watch: {
    todos: {
      handler: function (newValue, oldValue) {
        this.modifiedTodos = this.modifyTodos()
      },
      deep: true
    }
  },
  data () {
    return {
      todos: [],
      modifiedTodos: [],
      newTodoText: null,
      editTodoText: null,
      editIndex: null,
      editMode: false
    }
  },
  computed: {
    showTodoLeft () {
      return this.todos.length > 0
    }
  },
  methods: {
    addTodo () {
      this.todos.push(this.newTodoText)
      this.newTodoText = null
    },
    editTodo (index) {
      this.editMode = true
      this.editIndex = index
      this.editTodoText = this.todos[index]
    },
    updateTodo (index) {
      this.todos[index] = this.editTodoText
      this.editMode = false
      this.editIndex = null
      this.editTodoText = null
      
    },
    deleteTodo (index) {
      this.todos.splice(index, 1)
    },
    modifyTodos () {
      let modifiedTodos = []
      for (let i = 0; i < this.todos.length; i++) {
        let todo = this.todos[i]
        let todoWordArray = todo.split(' ')
        for (let j = 0; j < todoWordArray.length; j++) {
          let number = parseInt(todoWordArray[j])
          console.log('number', number)
          if (!isNaN(number)) {
            switch (number) {
              case 1:
                todoWordArray[j] = 'one'
                break
              case 2:
                todoWordArray[j] = 'two'
                break
              case 3:
                todoWordArray[j] = 'three'
                break
              case 4:
                todoWordArray[j] = 'four'
                break
              case 5:
                todoWordArray[j] = 'five'
                break
              case 6:
                todoWordArray[j] = 'six'
                break
              case 7:
                todoWordArray[j] = 'seven'
                break
              case 8:
                todoWordArray[j] = 'eight'
                break
              case 9:
                todoWordArray[j] = 'nine'
                break
              case 0:
                todoWordArray[j] = 'zero'
                break
            }
          }
        }
        todoWordArray = todoWordArray.join(' ')
        modifiedTodos.push(todoWordArray)
      }
      return modifiedTodos
    }
  }
}
</script>

<style scoped>
li {
  margin: 20px;
  padding: 20px;
  border: 1px solid black;
}
</style>
