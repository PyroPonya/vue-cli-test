<template>
  <div class="modal">
    <p class="modal__title">Добавление&nbsp;пользователя</p>
    <div class="modal__close" @click="closeModal()">x</div>
    <label for="userName">Имя</label>
    <input type="text" name="userName" id="userName" v-model="userName" />
    <label for="userPhone">Телефон</label>
    <input type="text" name="userPhone" id="userPhone" v-model="userPhone" />
    <label for="userChief">Начальник</label>
    <select name="userChief" id="userChief" v-model="userChief">
      <option value="">none</option>
      <option :value="el.id" v-for="(el, i) in userList" :key="i">{{
        el.name + " || " + el.phone
      }}</option>
    </select>
    <button class="btnSave" @click="passForm(userName, userPhone, userChief)">
      Сохранить
    </button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      userName: '',
      userPhone: '',
      userChief: ''
    }
  },
  props: ['userList'],
  methods: {
    passForm (name, phone, chief) {
      let newPerson = {
        id: '',
        name: name,
        phone: phone,
        parent: chief || ''
      }
      this.$emit('newPerson', newPerson)
    },
    closeModal () {
      this.$emit('closeModal', false)
    }
  }
}
</script>

<style scoped>
.modal {
  display: grid;
  grid-template-columns: 1fr 1fr;
  min-width: 200px;
  min-height: 200px;
  gap: 5px;
  border: 1px solid black;
}
.modal__close {
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid salmon;
}
.btnSave {
  cursor: pointer;
}
</style>
