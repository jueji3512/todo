<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ reminder }}</strong></span
    >
    <ul class="filters" @click="selectFn">
      <li>
        <a
          :class="{ selected: isSelected === 'all' }"
          href="javascript:;"
          @click="isSelected = 'all'"
          >全部</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isSelected === 'no' }"
          href="javascript:;"
          @click="isSelected = 'no'"
          >未完成</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isSelected === 'yes' }"
          href="javascript:;"
          @click="isSelected = 'yes'"
          >已完成</a
        >
      </li>
    </ul>
    <button class="clear-completed" @click="clearFn">清除已完成</button>
  </footer>
</template>

<script>
export default {
  props: ["listCount"],
  computed: { 
    reminder() { // 计算剩余任务数（全部）
      return this.listCount.length;
    },
  },
  data() {
    return {
      isSelected: "all",
    };
  },
  methods: {
    selectFn() { // 处理筛选
      this.$emit("changeType", this.isSelected);
    },
    clearFn(){ // 处理清空已完成
      this.$emit("clear")
    }
  },
};
</script>