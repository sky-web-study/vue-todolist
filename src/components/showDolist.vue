<template>
  <div class="dolist" v-if="isActiveFlg">
    <h2 class="listTitle">☆Do☆</h2>
    <ul
      class="dolist-contents"
      v-for="(todo, index) in todoList"
      :key="todo.createDate"
    >
      <li>
        {{ index + 1 }}:
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
  methods: {
    checkTodo(index) {
      this.$emit("updateDonelist", this.todoList[index]);
      this.$emit("changeDoneFlg", true);
      this.todoList.splice(index, 1);

      if (this.todoList.length == 0) {
        this.$emit("changeFlg", false);
      }
    },
    removeTodo(index) {
      this.todoList.splice(index, 1);
      if (this.todoList.length == 0) {
        this.$emit("changeFlg", false);
      }
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
