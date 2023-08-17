<template>
  <form @submit="handleSubmit" class="">
    <input type="text" id="" v-model="title" />
    <input type="submit" value="" />
  </form>
</template>

<script>
import { ref } from 'vue'
export default {
  name: 'AddTodo',
  setup(props, context) {
    const title = ref('')
    const handleSubmit = (event) => {
      event.preventDefault()
      const id = Math.floor(Math.random() * 1000)
      const newTodo = {
        id,
        title: title.value,
        complete: false
      }
      context.emit('addTodo', newTodo)
      title.value = ''
    }
    return {
      title,
      handleSubmit
    }
  }
}
</script>

<style></style>
