<script setup>
import { ref } from 'vue'
const title = ref('My ToDo App')
const input = ref({
  todo: '',
  isDone: false
})
const todos = ref([
  {
    todo: 'vueをマスターする',
    isDone: true
  },
  {
    todo: '牛乳を買う',
    isDone: false
  },
  {
    todo: '家賃を払う',
    isDone: false
  }
])

const addTodo = () => {
  if (input.value.todo.trim() !== '') {
    todos.value.push({ ...input.value })
    input.value.todo = ''
    input.value.isDone = false
  }
}

const clearDoneTodos = () => {
  todos.value = todos.value.filter((todo) => !todo.isDone)
}
</script>

<template>
  <h1 :title="message">{{ title }}</h1>
  <input type="text" v-model="input.todo" />
  <div v-if="input.todo.length === 0">
    <p>todoを記入してください</p>
  </div>
  <div v-else>
    <button @click="addTodo">追加</button>
  </div>

  <button @click="clearDoneTodos">完了済みを削除する</button>
  <h2>Todoリスト</h2>
  <div>
    <div v-if="todos.length === 0">
      <p>todoはまだありません！</p>
    </div>
    <ul v-show="todos.length !== 0">
      <li v-for="(todo, index) in todos" :key="index">
        <p>
          <input type="checkbox" v-model="todo.isDone" />
          <span :class="{ 'todo-done': todo.isDone }">{{ todo.todo }}</span>
        </p>
      </li>
    </ul>
  </div>
</template>

<style>
body {
  background-color: #eee;
}

.todo-done {
  text-decoration: line-through;
}
</style>
