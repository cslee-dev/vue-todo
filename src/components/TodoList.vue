<template>
  <section>
    <transition-group tag="ul" name="list">
      <li v-for="(todoItem, index) in todoItems" :class="shadow" :key="todoItem">
        <i :class="checkBtn" aria-hidden="true"></i>
        {{ todoItem }}
        <span :class="remoteBtn" type="button" @click="removeTodo(todoItem, index)">
          <i :class="trashIcon" aria-hidden="true"></i>
        </span>
      </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  name: "TodoList",
  props: ['todoItems'],
  data() {
    return {
      shadow: 'shadow',
      checkBtn: ['checkBtn', 'fas', 'fa-check'],
      trashIcon: ['far', 'fa-trash-alt'],
      remoteBtn: 'removeBtn',

    }
  },
  methods: {
    removeTodo(todoItem, index) {
      console.log(todoItem, index);
      this.$emit('removeBtn', todoItem, index);
    }
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0;
  margin-top: 0;
  text-align: left;
}

li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}

.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}

.removeBtn {
  margin-left: auto;
  color: #de4343;
}

.list-enter-active, .list-leave-active {
  transition: all 1s;
}

.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
