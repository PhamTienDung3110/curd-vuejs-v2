<template>
  <div class='todo_container' @click="handleOpenModalDetail()">
    <p>{{ todo.todoName }}</p>
    <div class="todo_bottom" v-if="todo.numberTask != 0">
      <i class="el-icon-tickets"></i>
      <span>{{ todo.numberTaskDone }}/{{ todo.numberTask }}</span>
    </div>
  </div>
</template>

<script>
import { EventBus } from "../EventBus"

export default {
  name: "TodoEle",
  props: {
    todo: Object,
    indTodo: Number,
    indCard: Number,
  },
  methods: {
    handleOpenModalDetail() {
      EventBus.$emit('open-modal', { todo: this.todo, indTodo: this.indTodo, indCard: this.indCard });
    }
  }
};
</script>

<style scoped>
.todo_container {
  margin: 10px 15px;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
  padding: 3px 10px;
  cursor: pointer;
}

.todo_bottom {
  margin-bottom: 5px;
  color: rgb(134, 124, 124);
  font-size: 14px;
}

.todo_bottom span {
  margin-left: 4px;
}
</style>