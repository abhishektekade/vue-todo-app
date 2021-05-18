<template>
  <div>
    <h1>{{ title }}</h1>
  </div>
  <div>
    <form action="" @submit.prevent="formSubmitted">
      <input type="text" v-model="newTask" />
      <div class="below-search"><button>Add</button></div>
      <!-- <button @click="removeAll">Remove All</button> -->
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <h1 :class="{ done: todo.done }" @click="done(todo)">
          {{ todo.title }}
        </h1>
        <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    let newTask = ref("");
    let todos = ref([]);
    function formSubmitted() {
      todos.value.push({
        done: false,
        title: newTask.value,
      });
      newTask.value = "";
    }

    function done(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }
    // function removeAll(index) {}

    return {
      title: "Todo App",
      newTask,
      formSubmitted,
      todos,
      done,
      removeTodo,
      // removeAll,
    };
  },
};
</script>

<style>
* body {
  margin: 0;
  padding: 0;
  text-align: center;
}
li {
  list-style: none;
}
input {
  width: 80%;
  height: 25px;
  padding: 2px;
  font-size: 20px;
}
.done {
  text-decoration: line-through;
}
/* .below-search {
  height: 25px;
  width: 80%;
} */
button {
  height: 35px;
  width: 81%;
  padding: 5px;
  margin: 10px;
}
</style>
