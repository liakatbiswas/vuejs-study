<script setup>
import { reactive, ref, computed } from 'vue';

const todo = ref("");

const todos = reactive([
  {
    id: 1,
    title: 'Todo one',
    completed: false
  },
  {
    id: 2,
    title: 'Todo two',
    completed: true
  }

])

const checkedComplete = (index) => {
  todos[index].completed = !todos[index].completed
}


const removeTodo = (index) => {
  todos.splice(index, 1)
}


const addTodo = (index) => {

  if (todo.value === '') {
    return
  }
  todos.push({
    id: todos.length + 1,
    title: todo.value,
    completed: false
  })

  todo.value = ""

}

const countAllTodo = computed(() => {
  return todos.length
})

const countCompleteTodo = computed(() => {
  return todos.filter(todo => todo.completed).length
})
</script>

 

<template>
  <div class="mx-auto mt-16 max-w-md space-y-6 overflow-hidden rounded-lg border bg-white p-6 shadow-lg">
    <h1 class="text-center text-2xl font-bold uppercase text-gray-700">To Do List <span v-if="todos.length">
        ({{ countCompleteTodo }}/{{ countAllTodo }})</span></h1>

    <!-- {{ todos }} -->
    <!-- {{ todo }} -->

    <form @submit.prevent="addTodo()">
      <div class="flex items-center border-b-2 border-teal-500 py-2">
        <input v-model="todo" type="text" class="w-full border-none text-gray-700 focus:outline-none"
          placeholder="Add a task" />

        <button type="submit"
          class="flex shrink-0 border-4 bg-teal-500 px-3 py-2 text-sm text-white hover:border-teal-700 hover:bg-teal-700">Add</button>
      </div>
    </form>

    <ul v-if="todos.length">
      <li v-for="(todo, index) in todos" :key="todo.id">

        <div class="flex items-center justify-between">
          <div class="flex items-center">
            <input type="checkbox" name="" class="h-4 w-4 rounded border-gray-300 text-teal-600 focus:ring-teal-500"
              :id="`todo-${todo.id}`" :checked="todo.completed" @input="checkedComplete(index)" />
            <label :for="`todo-${todo.id}`" class="ml-3 block text-gray-900" :class="{ 'line-through': todo.completed }">
              <span class="text-lg font-medium">{{ todo.title }}</span>
            </label>
          </div>

          <button @click="removeTodo(index)" class="flex">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
              stroke="currentColor" class="h-6 w-6">
              <path stroke-linecap="round" stroke-linejoin="round"
                d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
            </svg>
          </button>
        </div>
      </li>
    </ul>

    <div v-else>
      <p>No tasks yes.</p>
    </div>

  </div>
</template>



<style scoped></style>
