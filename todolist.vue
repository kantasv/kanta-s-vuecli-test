<template>
  <div class="app-wrapper">
    <h1 class='title'>ToDo List</h1>
    <h6>Powered by Kanta Yamaoka.</h6>


    <div class="input-wrapper">
      <input
        v-model="newToDoItem"
        v-on:keyup.ctrl.enter="addItem"
        placeholder="ToDoリストを入力"
      />
      <button @click="addItem" class="white-button">追加</button>
    </div>

    <h2>
      未完了
    </h2>
    <p v-if="!toDoItems.length" class='message'>・ToDo リストはありません</p>
    <p v-if="showsEmplyContentAlert" class='message'>
      ・空白のToDoリストは作成できません
    </p>
    <div v-for="(toDoItem, index) in toDoItems" v-bind:key="index">
      <div class="list">
        <p>{{ toDoItem }}</p>
        <button @click="deleteToDoList(index)" class="white-button">
          削除
        </button>
        <button @click="markToDoListAsDone(index)" class="blue-button">
          完了
        </button>
      </div>
    </div>
    <h2>
      完了済み
    </h2>

    <p v-if="!toDoItemsDone.length" class='message'>・完了済みの ToDo リストはありません</p>
    <div v-for="(toDoItemDone, index) in toDoItemsDone" v-bind:key="index">
      <div class='list'>
        <p>{{ toDoItemDone
        }}</p>
        <button @click="deleteToDoListDone(index)" class="white-button">
          削除
        </button>
        <button @click="markToDoListAsPending(index)" class="blue-button">
          未完了
        </button>
      </div>
    </div>


  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "BootstrapVue",
      show: true,
      newToDoItem: "",
      toDoItems: [],
      toDoItemsDone: [],
      showsEmplyContentAlert: false,
    };
  },
  methods: {
    addItem() {
      if (this.newToDoItem) {
        this.toDoItems.push('・'+this.newToDoItem);
        this.newToDoItem = "";
        this.showsEmplyContentAlert = false;
      } else {
        this.showsEmplyContentAlert = true;
      }
    },
    deleteToDoList(index) {
      this.toDoItems.splice(index, 1);
    },
    deleteToDoListDone(index) {
      this.toDoItemsDone.splice(index, 1);
    },
    markToDoListAsDone(index) {
      this.toDoItemsDone.push(this.toDoItems[index]);
      this.toDoItems.splice(index, 1);
    },
    markToDoListAsPending(index) {
      this.toDoItems.push(this.toDoItemsDone[index]);
      this.toDoItemsDone.splice(index, 1);
    }
  },
};
</script>

<style>
*:focus {
  outline: none;
}

.app-wrapper {
  width: 400px;
  height: 80%;
  background-color: white;
  margin: 10% auto;
  padding: 30px;
  border-radius: 20px;
  border: 1px solid #e6ecf0;

  /*#00acee;*/
}

button {
  margin-left: 5px;
  margin-right: 5px;
  float: right;
  width: 100px;
  height: 30px;
  border-radius: 25px;
  font-weight: bold;
  font-size: 12px;
}

.blue-button {
  background-color: #00acee;
  color: white;
  border: 1px solid #00acee;
}

.white-button {
  background-color: white;
  color: #00acee;
  border: 1px solid #00acee;
}

input {
  padding-left: 10px;
  background-color: #f6f8fa;
  border: none;
  font-size: 12px;
  height: 30px;
  width: 69%;
  border-bottom: 2px solid #657787;
}

input:focus {
  border-bottom: 2px solid #00acee;
}

.input-wrapper {
  background-color: white;
}

.list {
  background-color: #f6f8fa;
  width: 100%;
  height: 90px;
  margin-bottom: 5px;
}

.list p {
  padding: 5px;
}

.message{
  border:1px solid #00acee;
  text-align:center;
  line-height:50px;
  height:50px;
  color:#00acee;
}

h2{
  border-bottom: double 6px #00acee;
}

.title{
  color:#00acee;
}
</style>
