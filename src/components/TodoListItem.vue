<template>
    <div class="todo-item" :class="{'todo-item--done': todoItem.status === status.done}">
        <div class="todo-item__text">{{todoItem.todoText}}</div>
        <div class="todo-item__action">
            <span v-show="todoItem.status === status.active"
                @click="completeTodo">Klarmarkera</span>
            <span @click="deleteTodo">Ta bort</span></div>
    </div>
</template>

<script>
export default {
  name: 'TodoListItem',
  data () {
    return {
      isEditing: false,
      status: {
        done: 0,
        active: 1
      }
    };
  },
  props: {
    todoItem: Object
  },
  methods: {
    deleteTodo () {
      this.$emit('delete', this.todoItem.id);
    },
    completeTodo () {
      this.$emit('complete', this.todoItem.id);
    }
  }
}
</script>

<style lang="scss" scoped>
.todo-item {
  border: solid 1px black;
  margin-bottom: 10px;
  padding: 5px;
  display: flex;
  justify-content: space-between;
  &--done {
    color: white;
    border-color: green;
    background: rgb(74, 167, 67);
  }
  &__action {
    cursor: pointer;
    display: inline-flex;
    & span:first-child {
      margin-right: 10px;
    }
    & span:hover {
      text-decoration: underline;
    }
  }
}
</style>
