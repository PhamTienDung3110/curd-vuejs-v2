<template>
  <div class="card_container">
    <div class="card_top">
      <span>{{ listTodo.name }}</span>
      <span><i class="el-icon-more"></i></span>
    </div>
    <div class="card_todo" v-for="(ele, index) in listTodo.listTodo" :key="index">
      <TodoEle :todo="ele" :indTodo="index" :indCard="indCard" />
    </div>
    <div class="card_bottom" v-if="openAddTodo === false">
      <div class="card_bottom-add" @click="handleOpenAddTodo">
        <i class="el-icon-plus"></i><span>Add a todo</span>
      </div>
      <div class="card_bottom-template"><i class="el-icon-bangzhu"></i></div>
    </div>
    <div class="add-todo-input" v-if="openAddTodo === true">
      <input type="text" placeholder="Enter new Todo..." v-model="newTodo" />
      <div class="group-btn-todo">
        <button class="btn btn-add" @click="addTodo(listTodo.name)">Add</button>
        <button class="btn btn-cancel" @click="handleCloseAddTodo">X</button>
      </div>
    </div>
  </div>
</template>

<script>
import TodoEle from "./TodoEle.vue"
import { EventBus } from "../EventBus"

export default {
  name: 'CardTodo',
  data() {
    return {
      openAddTodo: false,
      newTodo: "",
      allTodos: this.allTodo,
    }
  },
  created() {
    EventBus.$on('delete-todo', (ind) => {
      console.log('abcd')
      console.log(this.allTodos)
      this.allTodos[ind.indCard].listTodo.splice(ind.indTodo, 1);
    });
  },
  methods: {
    handleOpenAddTodo() {
      this.openAddTodo = true;
    },
    handleCloseAddTodo() {
      this.openAddTodo = false;
      this.newTodo = "";
    },
    addTodo(nameCard) {
      const infoAddTodo = {
        newTodo: this.newTodo,
        nameCard: nameCard
      }
      this.$emit('addTodo', infoAddTodo);
      this.openAddTodo = false;
      this.newTodo = "";
    },
  },
  props: {
    listTodo: Object,
    indCard: Number,
    allTodo: Array,
  },
  components: {
    TodoEle
  }
}
</script>

<style scoped>
.card_container {
  width: 280px;
  height: auto;
  background-color: #EBECF0;
  border-radius: 4px;
}

.card_top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 7px 15px;
}

.card_bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 7px 15px;
}

.add-todo-input {
  width: 280px;
  height: 85px;
  border-radius: 4px;
  color: #fff;
  background-color: #EBECF0;
}

.add-todo-input input {
  width: 245px;
  height: 30px;
  margin-left: 13px;
  margin-top: 5px;
}

.group-btn-todo {
  margin: 5px 0 0 13px;
}
</style>
