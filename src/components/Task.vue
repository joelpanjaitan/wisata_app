<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="parentDiv">
      <div class="inputDiv">
        <input
          class="inputData"
          v-model="newTask"
          placeholder="Add task here"
          @keyup.enter="createTodo"
        /><button class="inputButton" @click="createTodo">add new</button>
      </div>
    </div>
    <p>
      For add todo project type input above,<br />
      check out the list below
    </p>
    <div class="todoList">
      <ul>
        <li class="liData" v-for="todo in activityList" :key="todo.id">
          <div class="liDisplay">
            <input type="checkbox" v-model="todo.completed" />
            <input
              v-if="todo.isEditing"
              v-model="todo.text"
              @blur="doneEditing(todo)"
              @keyup.enter="doneEditing(todo)"
              aria-label="Edit task"
            />
            <span v-else @click="editTodo(todo)">
              {{ todo.text }}
            </span>
            <button @click="deleteTodo(todo.id)">Remove</button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoTask",
  data() {
    return {
      newTask: "",
      activityList: [],
      activityId: 0,
    };
  },
  props: {
    msg: String,
  },
  methods: {
    createTodo() {
      if (this.newTask.trim() === "") return;
      this.activityList.push({
        id: this.activityId++,
        text: this.newTask,
        completed: false,
      });
      this.newTask = "";
    },
    editTodo(todo) {
      todo.isEditing = true;
    },
    doneEditing(todo) {
      if (todo.text.trim() === "") {
        this.removeTodo(todo.id);
      } else {
        todo.isEditing = false;
      }
    },
    deleteTodo(id) {
      this.activityList = this.activityList.filter((todo) => todo.id !== id);
    },
    clearTodo() {
      this.activityList = this.activityList.filter((todo) => !todo.completed);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.parentDiv {
  width: 100%;
  display: flex;
  justify-content: center;
}
.inputDiv {
  position: relative;
  width: 50%;
}
.inputData {
  width: 100%;
  border-color: rgb(156 163 175);
  border-width: 1px;
  border-radius: 20px;
  padding: 10px;
}
.inputButton {
  cursor: pointer;
  border-radius: 20px;
  padding-top: 9px;
  padding-bottom: 9px;
  position: absolute;
  right: -6%;
  top: 0;
}
.liDisplay {
  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 10px;
}
.liData {
  display: block;
}
.todoList {
  max-height: 30vh;
  overflow-y: auto;
}
</style>
