<template>
  <div id="app">
    <h1>ToDo's</h1>
    <form v-on:submit.prevent="saveNewTodo">
      <input type="text" id="new-todo" v-model="newTodo" placeholder="Todo">
      <input type="radio" id="high" value="High" name="priority" v-model="priority">
      <label for="high">High</label>
      <input type="radio" id="low" value="Low" name="priority" v-model="priority">
      <label for="low">Low</label>
      <input type="submit" value="Save Task">
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="index"
      :class="{ 'high': todo.priority === 'High', 'low': todo.priority === 'Low'}">
        <span>{{todo.name}}</span>
        <button @click="completeTask(index)">Complete</button>
        <span>{{todo.priority}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data(){
    return {
      todos: [
        {name: "Buy shopping", priority: "High"},
        {name: "Clean bathroom", priority: "Low"},
        {name: "Car's MOT", priority: "Low"}
      ],
      newTodo: ""
    }
  },
  methods: {
    saveNewTodo: function(){
      this.todos.push({
        name: this.newTodo,
        priority: this.priority
      });
      this.newTodo = ""
    },
    completeTask: function(index){
      this.todos.splice(this.todos.indexOf(index), 1);
      // this.todos[index].priority = "completed"
    }
  }
}
</script>

<style>
#app {
  width: 60%;
  margin: 0;
  padding: 20px;
  font-family:fantasy;
}
ul {
  margin: 10;
  list-style-type: none;
}
li {
  margin: 15px 0;
}
li.high {
  border: 2px solid;
  color: red;
}
li.low {
  border: 2px solid;
  color: yellow;
}
li.completed{
  border: 2px solid;
  color: green;
}
</style>