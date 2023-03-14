<script>
  export default {
    data() {
      return {
        newTask: '',
        tasks: []
      }
    },
    methods: {
      addTask() {
        if (this.newTask.trim() !== '') {
          this.tasks.push({
            name: this.newTask,
            done: false
          });
          this.newTask = '';
        }
      },
      deleteTask(index) {
        this.tasks.splice(index, 1);
      },
      deleteDoneTasks() {
        this.tasks = this.tasks.filter(task => !task.done);
      }
    }
  }
</script>

<template>
    <div>
      <h1 class="title">To do List</h1>
      <form @submit.prevent="addTask">
        <input type="text" v-model="newTask">
        <button type="submit">Ajouter</button>
      </form>
      <button class="foo" @click="deleteDoneTasks">Supprimer les tâches terminées</button>
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          <div class="todo">
            <input type="checkbox" v-model="task.done">
            <span :class="{ done: task.done }">{{ task.name }}</span>
          </div>
          <button class="del-btn" @click="deleteTask(index)">Supprimer</button>
        </li>
      </ul>
    </div>
</template>
  
<style>
body {
  background-color: #242424;
}
ul {
  padding: 0;
  margin-top: 35px;
}
.foo {
  margin-top: 10px;
}
.title {
  padding: 0 50px 5px;
  border: 1px solid #fff;
  border-radius: 5px;
}
.todo {
  margin-left: 5px;
}
.todo input {
  margin-right: 5px;
}
.del-btn {
  padding: 0.7em 1.2em;
  background-color: #6e0000;
  border-radius: 0 5px 5px 0;
}
li {
  width: 100%;
  margin: 10px;
  border: 1px solid #fff;
  border-radius: 5px;
  list-style: none;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
button img {
  height: 20px;
}
input[type=text] {
  height: 35px;
  margin-right: 25px;
}
.done {
text-decoration: line-through;
}
</style>
  