<template>
  <div class="container">
    <inputMenu @todoList="addList"></inputMenu>
    <showDolist
      :isActiveFlg="isActive"
      :todoList="list"
      @changeFlg="changeIsActive"
      @changeDoneFlg="changeIsDoneActive"
    ></showDolist>
    <showDonelist
      :isDoneActiveFlg="isDoneActive"
      :toDoneList="list"
      @changeFlg="changeIsActive"
      @changeDoneFlg="changeIsDoneActive"
    ></showDonelist>
  </div>
</template>

<script>
import inputMenu from "./components/InputMenu.vue";
import showDolist from "./components/showDolist.vue";
import showDonelist from "./components/showDonelist.vue";
export default {
  name: "App",
  components: {
    inputMenu,
    showDolist,
    showDonelist,
  },
  data() {
    return {
      isActive: false,
      isDoneActive: false,
      list: [],
    };
  },
  methods: {
    addList(value) {
      this.list.push({
        text: value,
        isDone: false,
        createDate: Date.now(),
      });
      this.isActive = true;
    },
    changeIsActive(value) {
      this.isActive = value;
    },
    changeIsDoneActive(value) {
      this.isDoneActive = value;
    },
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
</style>
