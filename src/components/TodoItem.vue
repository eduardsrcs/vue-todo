<template>
<li>
  <span 
    :class="{done: todo.completed,
    false: !todo.completed}"
  >
    <input
      type="checkbox"
      :checked="todo.completed"
      @change="todo.completed = !todo.completed"
    />
    <strong>{{index + 1}}</strong>
    {{todo.title | uppercase}}
  </span>
  <button
    class="rm"
    @click="$emit('remove-todo', todo.id)"
  >
    &times;
  </button>
</li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: {
      type: Number
    }
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase()
    }
  }
}
</script>

<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 1rem;
  margin-bottom: 1rem;
}

.rm {
  color: #fff;
  border-radius: 50%;
  background-color: #f33;
  font-weight: bold;
  outline: none;
}

.done {
  text-decoration: line-through;
}

input {
  margin-right: 1rem;
}


</style>