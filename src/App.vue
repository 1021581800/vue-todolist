<template>
  <div class="box">
    <el-input class="input" @keyup.enter="addTodo" v-model="inputValue" />
    <TodoList></TodoList>
  </div>
</template>

<script>
import TodoList from "./components/ToDoList.vue";
import { ref, watchEffect, provide } from 'vue'

export default {
  components: {
    TodoList
  },
  setup() {
    const inputValue = ref('')

    const cache = JSON.parse(localStorage.getItem("toDo"))
    const list = ref(cache || [])
    provide('list', list)
    function addTodo() {
      if (inputValue.value === "") {
        alert('请输入内容')
      }
      else {
        list.value.unshift({
          content: inputValue.value,
          isRed: false
        })
        inputValue.value = ""
      }
    }

    watchEffect(() => {
      const lists = JSON.stringify(list.value)
      localStorage.setItem('toDo', lists)
    })

    return {
      addTodo, inputValue
    }
  }
}
</script>

<style>
.box {
  width: 480px;
  margin: 0 auto;
}

.input {
  margin-bottom: 10px;
}
</style>