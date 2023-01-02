<template>
  <div id="app">
    <todo-list></todo-list>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import TodoList from '@/components/TodoList.vue'; // @ is an alias to /src

@Component({
  components: {
    TodoList,
  },
})
export default class Home extends Vue {}
</script>
