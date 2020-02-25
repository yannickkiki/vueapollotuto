<template>
  <ul>
    <li v-for="todo in todos" v-bind:key="todo.id">
      <div v-if="todo.is_public" class="userInfoPublic">
        @{{ todo.user.name }}
      </div>
      <div class="view" v-if="type === 'private'">
          <div v-if="todo.is_completed" class="round">
            <input
              type="checkbox"
              id="todo.id"
              checked="true"
            />
            <label 
              v-on:click="handleTodoToggle(todo)"
              htmlFor="todo.id"></label>
          </div>
          <div v-else class="round">
            <input
              type="checkbox"
              id="todo.id"
            />
            <label 
              v-on:click="handleTodoToggle(todo)"
              htmlFor="todo.id"></label>
          </div>
      </div>
      <div class="labelContent">
          <strike class="todoLabel" v-if="todo.is_completed">
            <div>
              {{ todo.title }}
            </div>
          </strike>
          <div v-else>
            {{ todo.title }}
          </div>
      </div>
      <button v-if="type === 'private'" v-on:click="handleTodoDelete(todo)" class="closeBtn"> x </button>
    </li>
  </ul>
</template>

<script>
    import gql from 'graphql-tag';
    const TOGGLE_TODO = gql`
   mutation update_todos($id: Int!, $isCompleted: Boolean!) {
    update_todos(where: { id: { _eq: $id } }, _set: { is_completed: $isCompleted }) {
       affected_rows
     }
   }
 `;
  export default {
    props: ['todos', 'type'],
    methods: {
      handleTodoToggle: function (todo) { // eslint-disable-line
        // update todo data in db here
      },
      handleTodoDelete: function(todo) { // eslint-disable-line
        // delete todo from db
      }
    }
  }

</script>
