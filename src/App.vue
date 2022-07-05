<template>
  <div id="app">
    <div class="list-card" v-for="(ele, index) in allTodo" :key="index">
      <CardTodo :listTodo="ele" @addTodo="addTodo" :indCard="index" :allTodo="allTodo"/>
    </div>
    <ModalTodo />
    <div class="add-card-text" v-if="openModalAddCard === false" @click="handleOpenAddCard">
      <p>+ Add another list</p>
    </div>
    <div class="add-card-input" v-if="openModalAddCard === true">
      <input type="text" placeholder="Enter new Card..." v-model="newCard" />
      <div class="group-btn">
        <button class="btn btn-add" @click="addCard">Add</button>
        <button class="btn btn-cancel" @click="handleCloseAddCard">X</button>
      </div>
    </div>
  </div>
</template>

<script>
import CardTodo from './components/CardTodo.vue';
import ModalTodo from './components/ModalTodo.vue';

export default {
  name: 'App',
  data() {
    return {
      allTodo: [
        {
          name: '1',
          listTodo: [
            {
              todoName: "toiec listening",
              numberTask: 3,
              numberTaskDone: 1,
              description: "tu page 10-40",
            },
            {
              todoName: "vuejs-udemy",
              numberTask: 5,
              numberTaskDone: 2,
              description: "lam assignment va video 30-34",
            },
            {
              todoName: "toiec reading",
              numberTask: 1,
              numberTaskDone: 1,
              description: "abcd",
            },
          ]
        },
        {
          name: '2',
          listTodo: [
            {
              todoName: "ielts listening",
              numberTask: 3,
              numberTaskDone: 1,
              description: "asdddddddddddddddddd",
            },
            {
              todoName: "reactjs-udemy",
              numberTask: 5,
              numberTaskDone: 2,
              description: "abcd",
            },
          ]
        }
      ],
      openModalAddCard: false,
      newCard: "",
    }
  },
  methods: {
    handleOpenAddCard() {
      this.openModalAddCard = true;
    },
    handleCloseAddCard() {
      this.openModalAddCard = false;
      this.newCard = "";
    },
    addCard() {
      this.allTodo.push({
        name: this.newCard,
        listTodo: []
      });
      this.newCard = "";
    },
    addTodo(infoAddTodo) {
      for (let i = 0; i < this.allTodo.length; i++) {
        if (this.allTodo[i].name === infoAddTodo.nameCard) {
          this.allTodo[i].listTodo.push({
            todoName: infoAddTodo.newTodo,
            numberTask: 0,
            numberTaskDone: 0,
            description: "",
          })
        }
      }
    }
  },
  components: {
    CardTodo,
    ModalTodo
  }
}
</script>

<style>
#app {
  display: flex;
}

.list-card {
  margin: 20px 10px;
}

.add-card-text {
  background-color: #565352;
  width: 280px;
  height: 40px;
  border-radius: 4px;
  color: #fff;
  margin: 20px 10px;
}

.add-card-text:hover {
  background-color: #656261;
}

.add-card-text p {

  margin: 10px 10px;
}

.add-card-input {
  width: 280px;
  height: 85px;
  border-radius: 4px;
  color: #fff;
  margin: 20px 10px;
  background-color: #EBECF0;
}

.add-card-input input {
  width: 255px;
  height: 30px;
  margin-left: 9px;
  margin-top: 5px;
}

.add-card-input .group-btn {
  display: flex;
  margin-left: 10px;
  margin-top: 5px;
}

.btn-add {
  background-color: #026AA7;
  border: none;
  border-radius: 3px;
  color: #fff;
  padding: 7px 12px;
  margin-right: 10px;
}

.btn-cancel {
  background-color: red;
  border: none;
  border-radius: 3px;
  color: #fff;
  padding: 7px 12px;
  margin-right: 10px;
}
</style>
