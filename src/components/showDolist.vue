<template>
  <div class="dolist" v-if="isActiveFlg">
    <h2 class="listTitle" v-if="isDoShow">☆Do☆</h2>
    <ul
      class="dolist-contents"
      v-for="(todo, index) in todoList"
      :key="todo.createDate"
    >
      <li v-if="!todo.isDone">
        <input type="checkbox" id="checkbox" @click="checkTodo(index)" />
        {{ todo.text }}<DeleteIcon @click="removeTodo(index)"></DeleteIcon>
      </li>
    </ul>
  </div>
</template>

<script>
import DeleteIcon from "vue-material-design-icons/Delete.vue";
export default {
  name: "showDolist",
  props: ["isActiveFlg", "todoList"],
  components: {
    DeleteIcon,
  },
  data() {
    return {
    };
  },
  computed: {
    isDoShow: function() {
      if(this.todoList.filter( todo => !todo.isDone ).length > 0) {
        return true;
      }else {
        return false;
      }
    }
  },
  methods: {
    checkTodo(index) {
      this.todoList[index].isDone = true;
      this.$emit("changeDoneFlg", true);
    },
    removeTodo(index) {
      this.todoList.splice(index, 1);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.dolist {
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

.dolist-contents {
  list-style: none;
  padding: 8px 32px;
  margin: 0px 16px;
}
</style>
