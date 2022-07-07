<template>
  <div id="app">
    <!--애플리케이션 이름 표시-->
    <todo-header></todo-header>
    <!--할일 입력 및 추가-->
    <todo-input v-on:addTodo="addTodo"></todo-input>
    <!--할 일 목록 표시 및 특정 할 일 삭제-->
    <todo-list v-bind:propsdata="todoItems" @removeTodo="removeTodo"></todo-list>
    <!--할 일 모두 삭제-->
    <todo-footer v-on:removeAll="clearAll"></todo-footer>
  </div>

</template>

<script>
import TodoHeader from "./components/TodoHeader";
import TodoInput from "./components/TodoInput";
import TodoList from "./components/TodoList";
import TodoFooter from "./components/TodoFooter";

export default {
  data() {
    return {
      todoItems: []
    }
  },
  methods: {
    // 인자값 todoItem = TodoInput 컴포넌트에서 올려 보낸 할 일 텍스트 값
    addTodo(todoItem) {
      // TodoInput 컴포넌트에서 App 컴포넌트로 신호(이벤트)를 보내 App 컴포넌트의 addTodo() 메서드를 실행
      localStorage.setItem(todoItem, todoItem);
      // App 컴포넌트의 todoItems 데이터 속성에 추가
      this.todoItems.push(todoItem);
    },
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    }

  },
  // 뷰의 인스턴스가 생성되자마자 뷰 데이터에 접근 할 수 있도록 created() 라이프 사이클 훅에서 로컬 스토리지의 데이터를 뷰 데이터로 옮김.
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++){
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  components: {
    'TodoHeader': TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}

</script>

<style>
  body{
    text-align: center;
    background-color: #F6F6F8;
  }
  input{
    border-style: groove;
    width: 200px;
  }
  button{
    border-style: groove;
  }
  .shadow{
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
