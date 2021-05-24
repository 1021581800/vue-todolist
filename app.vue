<template>
  <input id="inputEl" @keyup.enter="addTodo" />
  <button @click="addTodo">提交</button>
  <ul>
    <li
      :class="{ red: item.isRed }"
      v-for="(item,index) in lists"
      @click="changeColor(index)"
    >{{ item.content }}</li>
  </ul>
</template>
<style>
.red {
  color: red;
}
</style>
<script>


import { ref } from 'vue'
export default {
  setup() {
    const haveLists = JSON.parse(localStorage.getItem("toDo"))

    // hq start
    // let lists = ref(haveLists)
    // if (lists.value === null) lists = ref([])
    // hq end

    // let lists = haveLists === null ? ref([]) : ref(haveLists)

    // const lists = haveLists === null ? ref([]) : ref(haveLists)

    // const lists = ref(haveLists === null ? [] : haveLists)

    const lists = ref(haveLists || [])
    function addTodo() {
      const addvalue = document.querySelector('#inputEl').value
      if (addvalue === "") { alert('请输入内容') }
      else {
        lists.value.unshift({
          content: addvalue,
          isRed: false
        })
        cunchu(lists)
      }
      document.querySelector('#inputEl').value = ""
    }

    function changeColor(index) {
      lists.value[index].isRed = !lists.value[index].isRed
      cunchu(lists)
    }

    function cunchu(lists) {
      const listss = JSON.stringify(lists.value)
      localStorage.setItem('toDo', listss)
    }

    return {
      lists, addTodo, changeColor
    }
  }
}
</script>



