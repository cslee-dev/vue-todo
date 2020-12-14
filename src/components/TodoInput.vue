<template>
  <div :class="inputBoxClass">
    <input type="text" v-model="newTodoItem" placeholder="할일을 입력해보세요." @keyup.enter="addTodo">
    <span :class="addBtnClass" @click="addTodo">
      <i :class="addBtnIconClass" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="body" @click="showModal=false">
        할 일을 입력하세요.
        <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
      </span>
    </modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  name: "TodoInput",
  data() {
    return {
      showModal: false,
      newTodoItem: '',
      addBtnClass: 'addContainer',
      addBtnIconClass: ['addBtn', 'fas', 'fa-plus'],
      inputBoxClass: ['inputBox', 'shadow'],
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== "") {
        let value = this.newTodoItem && this.newTodoItem.trim();
        this.$emit('addItem', value);
        this.clearInput()
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
  },
  components:{
    'Modal':Modal,
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}

.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}

.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}

.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}

.addBtn {
  color: white;
  vertical-algin: middle;
}

</style>
