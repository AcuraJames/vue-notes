<template>
  <div>
    <h3>{{ name }}</h3>
    <div class="note-wrapper">
      <ul class="note">
        <li v-for="(todo, index) in todos" :key="index" class="note__item">
          <Checkbox :label="todo" />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import TODOS from '../todos.json'
import Checkbox from '../components/Checkbox'
export default {
  name: 'Note',
  components: {
    Checkbox
  },
  data() {
    return {
      name: "I'm new Todo",
      notes: TODOS || []
    }
  },
  computed: {
    noteId() {
      return this.$route.params.noteId
    },
    todos() {
      const todos = this.notes.find((note) => note.id === this.noteId)
      return todos.todos
    }
  }
}
</script>

<style lang="scss">
.note-wrapper {
  margin: auto;
  max-width: 300px;
}
.note {
  margin: auto;
  padding: 0;
  list-style-type: none;

  &__item {
    margin-bottom: 5px;
    text-align: left;
  }
}
</style>
