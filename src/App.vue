<script setup>
import { ref , onMounted,computed,watch } from 'vue'
const todos = ref([])
const name = ref('')
const input_content = ref('')
const input_category = ref(null)
const todos_asc = computed(() => todos.value.sort((a, b) =>
{
  return b.createdAT - a.createdAT
}))
watch(name, (newVal) => {
localStorage.setItem('name', newVal)
})
watch(todos, (newVal) => {
localStorage.setItem('todos', JSON.stringify(newVal))
}, {
  deep: true
})
onMounted(() => {
name.value = localStorage.getItem('name') || ''
todos.value = JSON.parse(localStorage.getItem('todos')) || []
})
const addTodo = () => {

  if (input_content.value.trim() === '' || input_category.value === null) {
    return
  }

  todos.value.push({
    content: input_content.value,
    category: input_category.value,
    done: false,
    editable: false,
    createdAt: new Date().getTime()
  })
}
const removeTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo)

}
onMounted(() => {
  name.value = localStorage.getItem('name') || ''
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})

</script>

<template>
  <main class="app">
    <section class="greeting">
      <h2 class="title">
        What's up <input type="text" id="name" placeholder="name here" v-model="name" />
      </h2>
    </section>
  </main>
</template>


