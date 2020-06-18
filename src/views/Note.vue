<template>
  <div>
    <input
      type="text"
      ref="title"
      class="title"
      :value="title"
      :placeholder="title"
      :disabled="!isTitleChanged"
      @input="changeTitle($event)"
    />
    <em @click="editTitle">&nbsp; i</em>
    <div class="note-wrapper">
      <ul class="note">
        <li v-for="(todo, index) in todos" :key="index" class="note__item">
          <Checkbox
            :label="todo.todo"
            :value="todo.done"
            @input="change($event, index)"
          />
        </li>
      </ul>
    </div>
    <button :disabled="!isChanged" @click="discard">
      Discard
    </button>
    <button :disabled="!isChanged" @click="save">
      Save
    </button>
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
      title: "I'm new Todo",
      newTitle: '',
      notes: TODOS || [],
      checked: [],
      unchecked: [],
      isChanged: false,
      isTitleChanged: false
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
  },
  methods: {
    editTitle() {
      this.isTitleChanged = true
      this.$refs.title.focus()
    },
    changeTitle(e) {
      // TODO confirm modal before change
      this.isChanged = true
      this.newTitle = e.target.value
    },
    change(val, index) {
      this.isChanged = true
      this.todos.map((todo, idx) => {
        if (idx === index) {
          todo.done = val
          val ? this.checked.push(todo) : this.unchecked.push(todo)
        }
      })
    },
    discard() {
      this.checked.map((todo) => (todo.done = false))
      this.unchecked.map((todo) => (todo.done = true))
      this.isChanged = false
    },
    save() {
      this.title = this.newTitle
      this.$router.push({ path: '/' })
    }
  }
}
</script>

<style lang="scss">
.title {
  font-size: 18px;
  font-weight: bold;
  color: forestgreen;
  border: none;
  background-color: transparent;

  &:focus {
    outline: none;
  }
}
.note-wrapper {
  margin: auto;
  margin-top: 30px;
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
