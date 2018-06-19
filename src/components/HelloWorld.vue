<template>
  <div>
    {{ msg }}
    <form>
      <button v-on:click="addTodo()">ADD TASK</button>
      <button v-on:click="removeTodo()">DELETE FINISHED TASKS</button>
      <p>input: <input type="text" v-model="newTodo"></p>
      <p>task:{{ newTodo }}</p>
    </form>
    <div class="task-list">
      <label class="task-list__item"
             v-for="todo in todos"
             v-bind:class="{ 'task-list__item--checked' : todo.done }" >
          <input type="checkbox" v-model="todo.done">
          <input type="checkbox" v-model="todo.editing">
          <input type="text"  v-if="todo.editing" v-model="todo.text" @keyup.enter="todo.editing = !todo.editing">
          <span v-else>{{todo.text}}</span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      todos : [
        {text : 'vue-router', done: false, editing : false},
        {text : 'vuex', done: false, editing : false},
        {text : 'vue-loader', done: false, editing : false},
        {text : 'awesome-vue', done: true, editing : false},
      ],
      newTodo : ""
    }
  },
  methods: {
    addTodo : function (event) {
      let text = this.newTodo && this.newTodo.trim()
      if (!text){
        return;
      }
      this.todos.push({
        text : text,
        done : false,
        editing : false,
      })
      this.newTodo = '';
    },
    removeTodo : function (event) {
      for ( let todoIndex = this.todos.length -1; todoIndex >= 0; todoIndex-- ) {
        if ( this.todos[ todoIndex ].done ) this.todos.splice(todoIndex,1);
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.task-list {
  display : flex;
  flex-direction: column;
  align-items: center;
}
.task-list__item,
.task-list__item--checked {
  width : 270px;
  text-align: left;
}
.task-list__item--checked {
  color : #85a6c6;
}
</style>
