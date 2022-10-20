<template>
  <div class="todoapp">
    <TodoHeader :arr="list" @create="createFn"></TodoHeader>
    <TodoMain :arr="showList" @del="deleteFn"></TodoMain>
    <TodoFooter
      :listCount="showList"
      @changeType="TypeFn"
      @clear="clearAll"
    ></TodoFooter>
  </div>
</template>

<script>
// 引入样式
import "./styles/base.css";
import "./styles/index.css";
// 引入组件
import TodoHeader from "./components/TodoHeader";
import TodoMain from "./components/TodoMain";
import TodoFooter from "./components/TodoFooter";

export default {
  components: { // 注册组件
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data() {
    return {
      list: JSON.parse(localStorage.getItem("todoList")) || [],
      getStr: "all",
    };
  },
  methods: {
    createFn(task) { // 添加任务
      let id =
        this.list.length === 0 ? 100 : this.list[this.list.length - 1].id + 1;
      this.list.push({
        id: id,
        name: task,
        isDone: false,
      });
    },
    deleteFn(delId) { // 删除任务
      let delIndex = this.list.findIndex((obj) => obj.id === delId);
      this.list.splice(delIndex, 1);
    },
    TypeFn(str) { // 接收当前点击的筛选
      this.getStr = str;
    },
    clearAll() { // 清除全部
      this.list = this.list.filter((obj) => obj.isDone === false);
    },
  },
  computed: {
    showList() {
      if (this.getStr === "yes") { // 显示已完成
        return this.list.filter((obj) => obj.isDone === true);
      } else if (this.getStr === "no") { // 显示未完成
        return this.list.filter((obj) => obj.isDone === false);
      } else { // 全部显示
        return this.list; 
      }
    },
  },
  watch: {
    list: {
      handler() {
        localStorage.setItem('todoList', JSON.stringify(this.list))
      },
      deep: true
    },
  },
};
</script>