<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fa fa-plus" aria-hidden="ture"></i>
    </span>

    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal = false">
        할 일을 입력하세요.
        <i class="closeModalBtn fa fa-times" aria-hidden="true"></i>
      </span>
    </modal>
  </div>
</template>

<script>
// Modal.vue 불러오기
import Modal from "./common/Modal";

export default {
  data() {
    return {
      newTodoItem: '',
      // 모달 동작을 위한 플래그 값
      showModal: false
    }
  },
  methods: {
    addTodo() {
      // 인풋 박스의 입력값이 있을 때만 저장
      if (this.newTodoItem !== ""){
        // 인풋 박스에 입력된 텍스트의 앞뒤 공백 문자열 제거
        var value = this.newTodoItem && this.newTodoItem.trim();
        // 입력받은 텍스트를 setItem() api를 이용해 로컬 스토리지에 데이터 추가(키값 형태)
        //localStorage.setItem(value, value);
        this.$emit('addTodo', value);
        // 인풋 박스의 입력 값을 초기화
        this.clearInput();
      } else {
        // 텍스트 미입력시 모달 동작
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
  },
  components: {
    // 모달 컴포넌트 등록
    Modal : Modal
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: inline-block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
</style>
