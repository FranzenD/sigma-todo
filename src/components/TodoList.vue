<template>
<div class="todo-list">
    <input type="text" class="todoInput" v-model="newTodo" @keyup.enter="addTodo" placeholder="Add todo..."/>

    <div v-for="todo in todoList" :key="todo.id">
        <todo-list-item :todo-item="todo"
                        @delete="deleteTodo"
                        @complete="completeTodo"></todo-list-item>
    </div>
    <div>Numer of todos: {{numberOfTodos}}</div>
</div>
</template>

<script>
import TodoListItem from './TodoListItem.vue';

let todoUid = 0;
const Status = {
  done: 0,
  active: 1
};

export default {
  name: 'TodoList',
  components: {
    TodoListItem
  },
  data () {
    return {
      todoList: [],
      newTodo: ''
    };
  },
  props: {},
  methods: {
    addTodo () {
      this.todoList.push({
        id: todoUid++,
        todoText: this.newTodo,
        status: Status.active
      });
      this.newTodo = '';
    },
    deleteTodo (todoId) {
      let index = this.todoList.findIndex(item => item.id === todoId);
      if (index > -1) {
        this.todoList.splice(index, 1);
      }
    },
    completeTodo (todoId) {
      this.todoList.find(item => item.id === todoId).status = Status.done;
    }
  },
  computed: {
    numberOfTodos () {
      return this.todoList.length;
    }
  }
};
</script>

<style lang="scss" scoped>
.todo-list {
  width: 60%;
  margin: 0 auto;
}
.todoInput {
  margin-bottom: 20px;
  width: 100%;
  padding: 10px;
  font-size: 24px;
  &:focus{
      outline: none;
  }
}
</style>
