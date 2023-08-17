<template>
  <body>
    <AddTodo @addTodo="handleAddTodo" />
    <Todo
      v-for="todo in todos"
      :key="todo"
      :todoProps="todo"
      @item-completed="handleChange"
      @deleteItem="handleDelete"
    />
  </body>
</template>

<script>
import Todo from './Todo/TodoItem.vue'
import AddTodo from './Todo/AddTodo.vue'
import { ref } from 'vue'
import axios from 'axios'

export default {
  name: 'Body',
  setup() {
    const todos = ref([])

    const getData = async () => {
      try {
        const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
        todos.value = res.data
      } catch (error) {
        console.log(error)
      }
    }
    getData()

    const handleChange = (id) => {
      todos.value = todos.value.map((item) => {
        if (item.id === id) {
          item.completed = !item.completed
        }
        return item
      })
    }
    const handleDelete = async (id) => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        todos.value = todos.value.filter((item) => item.id !== id)
      } catch (error) {
        console.log(error)
      }
    }

    const handleAddTodo = async (newTodo) => {
      try {
        const res = await axios.post(`https://jsonplaceholder.typicode.com/todos`, newTodo)
        todos.value.push(res.data)
      } catch (error) {
        console.log(error)
      }
    }

    return {
      todos,
      handleChange,
      handleDelete,
      handleAddTodo
    }
  },
  components: {
    Todo,
    AddTodo
  }
}
</script>

<style></style>
