<template>
  <div id="app">
    <div class="ToDo">
      <img class="Logo" src="../assets/vtCut.png" alt="Vue logo">
      <h1 class="ToDo-Header">Vue-TS To Do</h1>
      <div class="ToDo-Container">
        <div class="ToDo-Content">
          <ToDoItem v-for="todo in list" :todo="todo" @delete="onDeleteItem" :key="todo.id"/>
        </div>
        <input type="text" v-model="todo" v-on:keyup.enter="createNewToDoItem">
        <div class="ToDo-Add" @click="createNewToDoItem()">+</div>
      </div>
    </div>
  </div>
</template>


<script lang='ts'>
import ToDoItem from '../components/ToDoItem.vue'
import { Vue, Component, Prop } from 'vue-property-decorator' //vue.ts official library

interface ATodo {
  id: number
  text: string
}

@Component({
  components: { ToDoItem }
})
export default class ToDo extends Vue {
  @Prop() list: ATodo[] = [
    {
      id: 1,
      text: 'clean the house'
    },
    {
      id: 2,
      text: 'buy chocolates'
    }
  ]
  @Prop() todo: string = ''

  layout: string = 'addBar'

  createNewToDoItem() {
    if (!this.todo) {
      alert('Please enter a todo!')
      return
    }
    const newId = Math.max.apply(null, this.list.map((t: ATodo) => t.id)) + 1
    this.list.push({ id: newId, text: this.todo })
    this.todo = ''
  }

  onDeleteItem(todo: ATodo) {
    this.list = this.list.filter((item: ATodo) => item !== todo)
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  background: linear-gradient(#aeffae, #3d99ff);
  font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica,
    Arial, sans-serif;
  height: auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.Logo {
  width: 400px;
  padding: 10px;
  position: relative;
}

.ToDo {
  text-align: center;
  border: 1px solid white;
  width: 80vw;
  height: auto;
  box-shadow: 2px 3px 15px rgba(0, 0, 0, 0.5);
  background: #f6f6f6;
  padding-bottom: 60px;
  margin: 40px auto;
}

.ToDo-Header {
  color: black;
  font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica,
    Arial, sans-serif;
  font-weight: 400;
  text-transform: uppercase;
  margin: 30px auto 30px;
}

.ToDo-Add {
  color: white;
  font-size: 2em;
  width: 0.5em;
  height: 0.5em;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  cursor: pointer;
  background: #73ff73;
  border-radius: 10px;
  box-shadow: 1px 1px 1px #47a947;
  margin: 20px auto 0;
}

.ToDo-Add:hover {
  box-shadow: none;
  margin-top: 21px;
  /* margin-left: calc(auto + 1px); */
}

.ToDo-Container {
  width: 80%;
  margin: 0 auto;
}

input {
  width: 60%;
  padding: 10px;
  font-size: 1em;
  margin: 10px auto;
  box-shadow: 1px 3px 20px 0px rgba(0, 0, 0, 0.3);
}
</style>

