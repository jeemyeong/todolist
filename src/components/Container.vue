<template>
  <div>
    <todo-list
      v-bind:filteredTodoList="filteredTodoList"
      v-bind:leftItems="leftItems"
      v-on:toggleCheck="toggleCheck"
      v-on:destroyTodo="destroyTodo"
      v-on:toggleAll="toggleAll"
    />
    <!-- This footer should hidden by default and shown when there are todos -->
    <footer class="footer">
      <!-- This should be `0 items left` by default -->
      <span class="todo-count">
        <strong>{{ leftItems }}</strong> item left</span>
      <!-- Remove this if you don't implement routing -->
      <ul class="filters">
        <li>
          <a v-bind:class="{selected : filterStatus == Filter.ALL}" href="#/" v-on:click="adjustFilter(Filter.ALL)">All</a>
        </li>
        <li>
          <a v-bind:class="{selected : filterStatus == Filter.ACTIVE}" href="#/active" v-on:click="adjustFilter(Filter.ACTIVE)">Active</a>
        </li>
        <li>
          <a v-bind:class="{selected : filterStatus == Filter.COMPLETED}" href="#/completed" v-on:click="adjustFilter(Filter.COMPLETED)">Completed</a>
        </li>
      </ul>
      <!-- Hidden if no completed items are left ↓ -->
      <button class="clear-completed" v-on:click="clearCompleted">Clear completed</button>
    </footer>
  </div>
</template>

<script>
import TodoList from './TodoList.vue'
import { Filter } from '../constants/filter'

export default {
  name: 'Container',
  data() {
    return {
      Filter: Filter
    }
  },
  components: {
    'todo-list': TodoList
  },
  props: {
    filteredTodoList: Array,
    filterStatus: String,
    leftItems: Number
  },
  methods: {
    toggleCheck: function(todo) {
      this.$emit('toggleCheck', todo)
    },
    destroyTodo: function(index) {
      this.$emit('destroyTodo', index)
    },
    toggleAll: function() {
      this.$emit('toggleAll')
    },
    clearCompleted: function() {
      this.$emit('clearCompleted')
    },
    adjustFilter: function(filter) {
      this.$emit('adjustFilter', filter)
    }
  }
}
</script>

<style scoped>

</style>
