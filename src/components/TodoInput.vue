<template>
  <div :class="inputBoxClass">
    <input type="text" v-model="newTodoItem" placeholder="할일을 입력해보세요." @keyup.enter="addTodo">
    <span :class="addBtnClass" @click="addTodo">
      <i :class="addBtnIconClass" aria-hidden="true"></i>
    </span>
  </div>
</template>

<script>
export default {
  name: "TodoInput",
  data() {
    return {
      newTodoItem: '',
      addBtnClass: 'addContainer',
      addBtnIconClass: ['addBtn', 'fas', 'fa-plus'],
      inputBoxClass: ['inputBox', 'shadow'],
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== "") {
        var value = this.newTodoItem && this.newTodoItem.trim();
        localStorage.setItem(value, value);
        this.clearInput()
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
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
