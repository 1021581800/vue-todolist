<template>
  <div class="card-header" :class="{ red: item.isRed }" v-for="(item,index) in list" :key="item">
    <div class="list" @click="changeColor(index)">{{ item.content }}</div>
    <!-- <div class="deleteone">
      <i class="el-icon-delete deleteone" @click="deleteThis(index)"></i>
    </div>-->
    <i class="el-icon-delete deleteone" @click="deleteThis(index)"></i>
  </div>
</template>

<script>
import { ref, inject } from 'vue'
export default {

  setup(props) {
    const list = inject('list')
    //const list = ref(props.list)

    function changeColor(index) {
      list.value[index].isRed = !list.value[index].isRed
    }

    function deleteThis(index) {
      list.value.splice(index, 1)
    }

    return {
      list, changeColor, deleteThis
    }
  }
}
</script>

<style>
.deleteone {
  float: right;
}

.list {
  min-height: 20px;
  width: 460px;

  float: left;
  border-style: outset;
}
.red {
  color: red;
}
.card-header {
  font-size: 14px;
  text-align: center;
}
</style>