<template>
  <div class="todoapp">
    <toDoHeader @addTest="add" :arr="list"></toDoHeader>
    <toDoMain :list="showArr" @delTest="delA"></toDoMain>
    <toDoFooter
      :arr="showArr"
      @changeList="change"
      @cleanY="cleanYes"
    ></toDoFooter>
  </div>
</template>

<script>
import toDoHeader from "./components/TodoHeader.vue";
import toDoMain from "./components/TodoMain.vue";
import toDoFooter from "./components/TodoFooter.vue";

import "./style/base.css";
import "./style/index.css";

export default {
  components: {
    toDoHeader,
    toDoMain,
    toDoFooter,
  },
  data() {
    return {
      list: JSON.parse(localStorage.getItem("list")) || [],
      getSel: "all",
    };
  },
  methods: {
    add(obj) {
      this.list.push(obj);
    },
    delA(index) {
      this.list.splice(index, 1);
    },
    change(status) {
      //根据status筛选数据
      this.getSel = status;
    },
    cleanYes() {
      this.list = this.list.filter((obj) => obj.isDone === false);
    },
  },

  computed: {
    showArr() {
      if (this.getSel === "yes") {
        return this.list.filter((obj) => obj.isDone === true);
      } else if (this.getSel === "no") {
        return this.list.filter((obj) => obj.isDone === false);
      } else {
        return this.list;
      }
    },
  },
  watch: {
    list: {
      handler() {
        localStorage.setItem("list", JSON.stringify(this.list));
      },
      immediate: true,
      deep: true,
    },
  },
};
</script>

<style>
</style>
