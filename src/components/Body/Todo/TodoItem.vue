<template>
  <div class="wp-item-todo">
    <div class="item-todo">
      <input  type="checkbox" name="" id="" :checked="todoProps.completed" @change="handleChange" />
      <span :class="[todoProps.completed ? 'is-competed' : '']">{{ todoProps.title }}</span>
    </div>
    <button @click="handleDelete">Delete</button>
  </div>
</template>

<script>
//import { ref } from 'vue'
export default {
  name: 'Todo',
  props: ['todoProps'],
  setup(props, context) {
    const handleChange = () => {
      context.emit('item-completed', props.todoProps.id)
    }
    const handleDelete = () => {
      context.emit('deleteItem', props.todoProps.id)
    }
    return {
      handleChange,
       handleDelete
    }
  }
}
</script>

<style>
.wp-item-todo {
  width: 100%;
  height: 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid rgb(225, 225, 225);
  background-color: rgb(244, 241, 241);
  padding: 0 20px;
}
.wp-item-todo:hover {
  background-color: aliceblue;
}
.item-todo {
  display: flex;
  align-items: center;
  gap: 10px;
}
.is-competed {
  text-decoration: line-through;
}
.item-todo input {
}
</style>
