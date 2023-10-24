<style>
* {
  box-sizing: border-box;
}

ul {
  margin: 0;
  padding: 0;
}

ul li {
  cursor: pointer;
  position: relative;
  padding: 8px 8px 8px 40px;
  background: #eee;
  font-size: 14px;
  transition: 0.2s;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

ul li:hover {
  background: #ddd;
}

ul li.checked {
  background: #BBB;
  color: #fff;
  text-decoration: line-through;
}

ul li.checked::before {
  content: '';
  position: absolute;
  border-color: #fff;
  border-style: solid;
  border-width: 0px 1px 1px 0px;
  top: 10px;
  left: 16px;
  transform: rotate(45deg);
  height: 8px;
  width: 8px;
}

.close {
  position: absolute;
  right: 0;
  top: 0;
  padding: 8px 12px 8px 12px
}

.close:hover {
  background-color: #f44336;
  color: white;
}
</style>
<template>
  <ul id="todolist">
    <li v-for="a in todolist" :key="a.id" :class="checked(a.done)"
        @click="doneToggle({id : a.id})">
      <span>{{ a.todo }}</span>
      <span v-if="a.done"> (완료)</span>
      <span class="close" @click.stop="deleteTodo({id : a.id})">&#x00D7;</span>
    </li>
  </ul>
</template>
<script type="text/javascript">
import Constant from "@/Constant";
import {mapMutations, mapState} from "vuex";

export default {
  /*TODO: vuex 11장 로 저장하기*/

  name    : 'item-list',
  computed: mapState(['todolist']),
  methods : {
    checked: function (done) {
      if (done) return {checked: true};
      else return {checked: false};
    }
    ,
    doneToggle: function (id) {
      // 화면에서 일어나는 이벤트를 받아 처리하는 메서드에서 변의(mutation)를 일으키키 위해 메서드 호출
      // 첫 번째 인자는 변이의 이름.
      this.$store.commit(Constant.DONE_TOGGLE, {id:id})
      
    },
    deleteTodo: function (id) {
      this.$store.commit(Constant.DELETE_TODO, {id:id})
    },
    ...mapMutations([
    Constant.DELETE_TODO,
    Constant.DONE_TOGGLE
    ])
  }
}
</script>