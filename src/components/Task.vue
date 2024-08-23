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
    <span>{{ currentDate }}</span>
    <div class="todoList">
      <ul class="ulList">
        <li
          class="liData"
          v-for="todo in activityList"
          :key="todo.id"
          :ref="'item-' + todo.id"
        >
          <div class="liDisplay">
            <input
              v-if="todo.isEditing"
              v-model="todo.text"
              @blur="doneEditing(todo)"
              @keyup.enter="doneEditing(todo)"
              aria-label="Edit task"
              class="editTodoInput"
              ref="input"
            />
            <span
              class="todoSpan"
              :class="{ completedTask: todo.completed }"
              v-if="!todo.isEditing"
              @click="editTodo(todo)"
            >
              {{ todo.text }}
            </span>
            <button @click="setComplete(todo)" class="icon">
              <RiCheckFill />
            </button>
            <button @click="deleteTodo(todo.id)" class="icon">
              <RiDeleteBinLine />
            </button>
          </div>
        </li>
      </ul>
    </div>
    <div class="footer">
      <h1 class="text-3xl font-bold underline">Do your task!</h1>
      <button
        class="icon clearButton"
        v-if="activityList && activityList.length"
        @click="clearTodo"
        aria-label="Clear completed tasks"
      >
        Clear Completed
      </button>
    </div>
  </div>
</template>

<script>
import { RiDeleteBinLine } from "@remixicon/vue";
import { RiCheckFill } from "@remixicon/vue";
import { ref } from "vue";
export default {
  name: "TodoTask",
  data() {
    return {
      newTask: "",
      activityList: [],
      activityId: 0,
      currentDate: new Date().toLocaleString(),
    };
  },
  components: {
    RiDeleteBinLine,
    RiCheckFill,
  },
  props: {
    msg: String,
  },
  setup() {
    const input = ref(null);
    return { input };
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
      this.focustLastItem();
    },
    editTodo(todo) {
      todo.isEditing = true;
    },
    setComplete(todo) {
      if (todo.isEditing === true) {
        todo.isEditing = false;
        return;
      }
      todo.completed = !todo.completed;
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
    focustLastItem() {
      const lastItem = this.activityList[this.activityList.length - 1];
      if (lastItem) {
        this.$nextTick(() => {
          const lastItemRef = this.$refs["item-" + lastItem.id];
          if (lastItemRef && lastItemRef.length) {
            if (lastItemRef[0]) lastItemRef[0].scrollIntoView();
          }
        });
      }
    },
    clearTodo() {
      this.activityList = this.activityList.filter((todo) => !todo.completed);
    },
    updateDate() {
      this.currentDate = new Date().toLocaleString(); // Update the current date and time
    },
  },
  mounted() {
    this.updateDate();
    this.interval = setInterval(this.updateDate, 1000);
  },
  beforeUnmount() {
    clearInterval(this.interval);
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
.icon {
  border-radius: 20px;
  border-color: ghostwhite;
}
.clearButton {
  border-radius: 20px;
  padding: 0px 10px;
  height: 40px;
  cursor: pointer;
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
.todoSpan {
  width: 15vw;
  text-overflow: ellipsis;
  overflow: hidden;
  padding-left: 10px;
}
.editTodoInput {
  width: 14vw;
  margin-left: 1vw;
}
.liDisplay {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: 10px;
  padding-right: 10px;
}
.ulList {
  max-width: 30vw;
  gap: 2px;
}
.liData {
  display: block;
  padding: 5px 0px;
  background-color: #aeb1b4;
  margin-bottom: 5px;
  border-radius: 20px;
}
.todoList {
  display: flex;
  justify-content: center;
  max-height: 30vh;
  overflow-y: auto;
}
.footer {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
}
.completedTask {
  text-decoration: line-through;
}
</style>
