<style>
* {
  box-sizing: border-box;
}

.header {
  background-color: cornflowerblue;
  padding: 30px 30px;
  color: black;
  text-align: center;
}

.header:after {
  content: "";
  display: table;
  clear: both;
}
</style>
<template>
  <div id="todolist">
    <div id="header" class="header">
      <h2>기록하고, 잊지말아요~</h2>
      <input-todo/>
    </div>
    <item-list></item-list>
  </div>
</template>
<script type="text/javascript">
import InputTodo from './InputTodo';
import ItemList from "@/components/ItemList.vue";

export default {
  name      : 'todo-list',
  components: {InputTodo, ItemList}
}
</script>