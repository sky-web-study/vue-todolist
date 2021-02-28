<template>
    <div class="container">
      <inputMenu @todoList = "addList"></inputMenu>
      <div class="dolist" v-if="isActive">
        <h2 class="listTitle">☆Do☆</h2>
        <ul class="dolist-contents" v-for="(todo, index) in list" :key="todo.createDate">
          <li>{{ index + 1}}:
              <input type="checkbox" id="checkbox" @click="checkTodo(index)">
              {{ todo.text }}<DeleteIcon @click="removeTodo(index)"></DeleteIcon></li>
          <!-- <li class="dolist-item">
            <input type="checkbox" class="list-chk" />
            <span class="dolist-txt">1234567890</span>
            <button class="material-icons">delete</button>
          </li> -->
        </ul>
      </div>
      <div class="donelist" v-if="isDoneActive">
        <h2 class="listTitle">★Done★</h2>
        <ul class="donelist-contents" v-for="(todo, index) in donelists" :key="todo.createDate">
          <li>{{ index + 1}}:
              <input type="checkbox" id="checkbox" @click="checkDone(index)">
              {{ todo.text }}<DeleteIcon @click="removeDone(index)"></DeleteIcon></li>
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
import inputMenu from "./components/InputMenu.vue";
import DeleteIcon from 'vue-material-design-icons/Delete.vue';
export default {
  name: 'App',
  components: {
    inputMenu,
    DeleteIcon
  },
  data() {
    return {
      isActive: false,
      isDoneActive: false,
      list:[],
      donelists:[]
    };
  },
  methods: {
    addList(value) {
        this.list.push({
          text: value,
          createDate: Date.now(),
        });
        this.isActive = true;
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
</style>
