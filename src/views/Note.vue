<template>
  <div>
    <h3>Name</h3>
    <ul class="note">
      <li
        v-for="(todo, index) in todos" :key="index"
        class="note__item"
      >
        <Checkbox :label="todo" />
      </li>
    </ul>
  </div>
</template>

<script>
import Checkbox from '../components/Checkbox'
export default {
  name: 'Note',
  components: {
    Checkbox
  },
  data() {
    return {
      name: 'I\'m new Todo',
      todos: ['vossi bop', 'cinnabon', 'dossie doe', 'tasty toast', 'hopsey hoe', 'noisy nose'],
    }
  }
}
</script>

<style lang="scss">
.note {
  padding: 0;
  list-style-type: none;

  &__item {
    margin-bottom: 5px;
    text-align: left;
  }
}
</style>