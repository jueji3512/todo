<template>
  <header class="header">
    <h1>todo</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll" />
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keydown.enter="keydownFn"
      v-model="task"
    />
  </header>
</template>

<script>
export default {
  props: ["arr"],
  data() {
    return {
      task: "",
    };
  },
  methods: {
    keydownFn() {
      this.$emit("create", this.task);
      // 确认后，将输入框清空
      this.task = "";
    },
  },
  computed: {
    isAll: { // 处理全选
      set(checked) { // 因为input是checked类型，故参数为bool类型
        this.arr.forEach((obj) => (obj.isDone = checked));
      },
      get() { // 无数据不勾选，每个数据都true即勾选
        return (
          this.arr.length !== 0 && this.arr.every((obj) => obj.isDone === true)
        )
      },
    },
  },
};
</script>