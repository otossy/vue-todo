<template>
  <div class="box_input">
    <input
      v-model="todoRef"
      type="text"
      class="todo_input"
      placeholder="+ TODOを入力"
    />
    <button class="btn" @click="addTodo">追加</button>
  </div>
</template>

<script>
// import { ref } from "vue";
// const todoRef = ref("");
export default {
  data: () => {
    return {
      todoRef: '',
      todoListRef: [],
    };
  },
  methods: {
    addTodo() {
      localStorage.todoList = this.todoRef;
      const id = new Date().getTime();
      this.todoListRef.push({id: id, task: this.todoRef});
      localStorage.todoList = JSON.stringify(this.todoListRef);
      this.todoRef = '';
    }
  },
};
</script>

<style>
.box_input {
  margin-top: 20px;
}

.todo_input {
  width: 300px;
  margin-right: 8px;
  padding: 8px;
  font-size: 18px;
  border: 1px solid #aaa;
  border-radius: 6px;
}

.btn {
  padding: 8px;
  background-color: #03a9f4;
  border-radius: 6px;
  color: #fff;
  text-align: center;
  font-size: 14px;
}
</style>
