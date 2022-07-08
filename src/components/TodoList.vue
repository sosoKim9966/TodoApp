<template>
  <section>
    <transition-group name="list" tag="ul">
      <!--:key => v-for 디렉티브를 사용할 때 꼭 지정해주는 것이 좋다.-->
      <li v-for="(todoItem, index) in propsdata" :key="todoItem" class="shadow">
          <i class="checkBtn fa fa-check" aria-hidden="true"></i>
          {{ todoItem }}
          <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)">
            <i class="far fa-trash-alt" aria-hidden="true"></i>
          </span>
      </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  props: ['propsdata'],
  methods: {
    removeTodo(todoItem, index) {
      // removeItem() -> todoItem 인자를 사용하여 로컬 스토리지에서 할 일 텍스트 삭제
      //localStorage.removeItem(todoItem);
      // splice() -> 인자로 받은 index를 이용하여 배열의 해당 인덱스에서 1만큼 삭제
      //this.todoItems.splice(index,1);
      this.$emit('removeTodo', todoItem, index);
    }
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
