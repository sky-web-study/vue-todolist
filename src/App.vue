<template>
    <div class="container">
      <div class="inputMenu">
        <h1 class="inputMenuTitle">{{ title }}</h1>
        <input
          name="todo"
          type="text"
          v-model="todoItem"
          v-on:keyup.enter="addText"
          placeholder="Todoを入力してください。"
          id="todoInput"
        />
      </div>
      <div class="dolist" v-if="isActive">
        <h2 class="listTitle">{{ dolist }}</h2>
        <ul class="dolist-contents" v-for="(todo, index) in list" v-bind:key="index">
          <li>{{ index + 1}}:
              <input type="checkbox" id="checkbox" v-model="checked" v-on:click="checkTodo(index)">
              {{ todo.text }}<button v-on:click="removeTodo(index)">delete</button></li>
          <!-- <li class="dolist-item">
            <input type="checkbox" class="list-chk" />
            <span class="dolist-txt">1234567890</span>
            <button class="material-icons">delete</button>
          </li> -->
        </ul>
      </div>
      <div class="donelist" v-if="isDoneActive">
        <h2 class="listTitle">{{ donelist }}</h2>
        <ul class="donelist-contents" v-for="(todo, index) in donelists" v-bind:key="index">
          <li>{{ index + 1}}:
              <input type="checkbox" id="checkbox" v-model="doneChecked" v-on:click="checkDone(index)">
              {{ todo.text }}<button v-on:click="removeDone(index)">delete</button></li>
          <!-- <li class="donelist-item">
            <input type="checkbox" class="list-chk" />
            <span class="donelist-txt">123456789012345678901234567890</span>
            <button class="material-icons">delete</button>
          </li> -->
        </ul>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      title: "Todo List",
      isActive: false,
      isDoneActive: false,
      dolist: "☆Do☆",
      donelist: "★Done★ ",
      todoItem: '',
      list:[],
      donelists:[],
      checked: false,
      doneChecked: true
    };
  },
  methods: {
    addText() {
      if(this.todoItem){
        this.list.push({
          text: this.todoItem,
        });
        this.isActive = true;
      }
      this.todoItem = '';
    },
    checkTodo(index) {
      this.donelists.push(this.list[index]);
      this.isDoneActive = true;
      this.list.splice(index, 1);
      if(this.list.length == 0){
        this.isActive = false;
      }
    },
    removeTodo(index) {
      this.list.splice(index, 1);
      if(this.list.length == 0){
        this.isActive = false;
      }
    },
    checkDone(index){
      this.list.push(this.donelists[index]);
      this.isActive = true;
      this.donelists.splice(index, 1);
      if(this.donelists.length == 0){
        this.isDoneActive = false;
      }
    },
    removeDone(index) {
      this.donelists.splice(index, 1);
      if(this.donelists.length == 0){
        this.isDoneActive = false;
      }
    }
  },
};
</script>

<style>
  html {
    background-color: #ffe4b5;
  }
</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  background-color: white;
  width: 80%;
  border-radius: 16px;
  margin: 160px auto 0px auto;
}

.inputMenu {
  height: 120px;
  padding: 8px 32px;
  user-select: none;
}

.inputMenuTitle {
  font-size: 24px;
  margin: 16px 8px;
}

#todoInput {
  width: 95%;
  font-size: 16px;
  margin-bottom: 16px;
  outline: none;
}

.dolist,
.donelist {
  width: 100%;
  margin: 0px auto;
  /* display: none; */
  user-select: none;
}

.listTitle {
  font-size: 20px;
  margin: 0px 8px;
  padding-left: 32px;
  background-color: white;
}

.dolist-contents,
.donelist-contents {
  list-style: none;
  padding: 8px 32px;
  margin: 0px 16px;
}

/* .dolist-item,
.donelist-item {
  display: flex;
  align-items: flex-start;
  padding-bottom: 16px;
} */

/* .list-chk {
  margin-right: 16px;
} */

/* .dolist-txt,
.donelist-txt {
  word-break: break-all;
} */

/* .material-icons {
  color: grey;
  background-color: white;
  cursor: pointer;
  margin-left: 16px;
  padding: 0;
  border: none;
} */
</style>
