<template>
  <div class="donelist" v-if="isDoneActiveFlg">
    <h2 class="listTitle">★Done★</h2>
    <ul
      class="donelist-contents"
      v-for="(todo, index) in toDoneList"
      :key="todo.createDate"
    >
      <li v-if="todo.isDone">
        {{ index + 1 }}:
        <input type="checkbox" id="checkbox" @click="checkDone(index)" />
        {{ todo.text }}<DeleteIcon @click="removeDone(index)"></DeleteIcon>
      </li>
    </ul>
  </div>
</template>

<script>
import DeleteIcon from "vue-material-design-icons/Delete.vue";
export default {
  name: "showDonelist",
  props: ["isDoneActiveFlg", "toDoneList"],
  components: {
    DeleteIcon,
  },
  data() {
    return {
    };
  },
  methods: {
    checkDone(index) {
      this.toDoneList[index].isDone = false;
      this.$emit("updateDolist", this.toDoneList[index]);
      this.$emit("changeFlg", true);
      this.toDoneList.splice(index, 1);

      if (this.toDoneList.length == 0) {
        this.$emit("changeDoneFlg", false);
      }
    },
    removeDone(index) {
      this.toDoneList.splice(index, 1);
      if (this.toDoneList.length == 0) {
        this.$emit("changeDoneFlg", false);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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

.donelist-contents {
  list-style: none;
  padding: 8px 32px;
  margin: 0px 16px;
}
</style>
