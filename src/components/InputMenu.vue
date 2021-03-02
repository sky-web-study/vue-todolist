<template>
  <div class="inputMenu">
    <h1 class="inputMenuTitle">Todo List</h1>
    <input
      name="todo"
      type="text"
      v-model="todoItem"
      v-on:keyup.enter="ipnutText"
      placeholder="Todoを入力してください。"
      id="todoInput"
    />
  </div>
</template>

<script>
export default {
  name: "InputMenu",
  data() {
    return {
      todoItem: "",
    };
  },
  methods: {
    ipnutText() {
      if (this.todoItem) {
        this.$emit("todoList", this.todoItem);
      }
      this.todoItem = "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
</style>
