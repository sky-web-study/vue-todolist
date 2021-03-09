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
    <p class="error-todo" v-show="!isValid">※Todoの項目が未入力です</p>
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
  computed: {
    isValid: function () {
      let valid = true;
      if(this.todoItem.length < 1){
        valid = false;
      }
      return valid;
    },
  },
  methods: {
    ipnutText() {
      if(this.isValid) {
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
  margin-bottom: 4px;
  outline: none;
}

.error-todo {
  margin-top: 0;
  color: red;
}
</style>
