<template>
  <div class="box_input">
    <input
      v-model="todoRef"
      type="text"
      class="todo_input"
      placeholder="+ TODOを入力"
    />
    <button class="btn green" @click="editTodo" v-if="isEditRef">変更</button>
    <button class="btn" @click="addTodo" v-else>追加</button>
  </div>
  <div class="box_list">
    <div class="todo_list" v-for="todo in todoListRef" :key="todo.id">
      <div class="todo">
        <input type="checkbox" class="check" /><label>{{ todo.task }}</label>
      </div>
      <div class="btns">
        <button class="btn green" @click="showTodo(todo.id)">編</button>
        <button class="btn pink">削</button>
      </div>
    </div>
  </div>
</template>

<script>
// import { ref } from "vue";
// const todoRef = ref("");
export default {
  data: () => {
    return {
      todoRef: '',
      todoListRef: JSON.parse(localStorage.todoList),
      isEditRef: false,
      editTodo: () => {}
    };
  },
  methods: {
    addTodo() {
      localStorage.todoList = this.todoRef;
      const id = new Date().getTime();
      this.todoListRef.push({id: id, task: this.todoRef});
      localStorage.todoList = JSON.stringify(this.todoListRef);
      this.todoRef = '';
    },
    showTodo(id) {
      const todo = this.todoListRef.find((todo) => todo.id === id);
      this.todoRef = todo.task;
      this.isEditRef = true;
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

.box_list {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.todo_list {
  display: flex;
  align-items: center;
  gap: 8px;
}

.todo {
  border: 1px solid #ccc;
  border-radius: 6px;
  padding: 12px;
  width: 300px;
}

.check {
  border: 1px solid red;
  transform: scale(1.6);
  margin: 0 16px 2px 6px;
}

.btns {
  display: flex;
  gap: 4px;
}

.green {
  background-color: #00c853;
}

.pink {
  background-color:  #ff4081;
}
</style>
