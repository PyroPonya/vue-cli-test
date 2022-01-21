<template>
  <div id="app">
    <button class="btn" @click="modalShow = !modalShow">Добавить</button>
    <List class="list" :userList="userList" />
    <Modal
      class="modal"
      v-if="modalShow == true"
      :userList="userList"
      @closeModal="modalShow = false"
      @newPerson="addPerson($event)"
    />
  </div>
</template>

<script>
import List from './components/List.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    List,
    Modal
  },
  mounted () {
    if (localStorage.userListStored) { this.userList = JSON.parse(localStorage.userListStored) }
  },
  data () {
    return {
      modalShow: false,
      // userList: [
      //   {
      //     id: 1,
      //     name: 'name1',
      //     phone: 'phone1',
      //     parent: ''
      //   },
      //   {
      //     id: 2,
      //     name: 'name2',
      //     phone: 'phone2',
      //     parent: ''
      //   },
      //   {
      //     id: 3,
      //     name: 'name3',
      //     phone: 'phone3',
      //     parent: ''
      //   },
      //   {
      //     id: 4,
      //     name: 'name4',
      //     phone: 'phone4',
      //     parent: 1
      //   },
      //   {
      //     id: 5,
      //     name: 'name5',
      //     phone: 'phone5',
      //     parent: 3
      //   }
      // ]
      userList: []
    }
  },
  methods: {
    getNewId (arr) {
      let lastId = 0
      arr.map(el => {
        if (el.id > lastId) lastId = el.id
      })
      return lastId
    },
    addPerson (person) {
      let newId = this.getNewId(this.userList) + 1
      person.id = newId
      this.userList.push(person)
      localStorage.setItem('userListStored', JSON.stringify(this.userList))
    }
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: grid;
  grid-template-areas:
    "btn btn"
    "list modal";
  gap: 25px;
}
.btn {
  height: 30px;
  width: 150px;
  background-color: rgba(128, 128, 128, 0.534);
  border-radius: 15px;
  cursor: pointer;
  grid-area: btn;
}
.list {
  grid-area: list;
}
.modal {
  grid-area: modal;
}
</style>
