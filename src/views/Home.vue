<template>
  <div class="home">
    <ConfirmModal v-if="showModal" @confirm="confirm" @deny="deny">
      <template v-slot:header>Удалить запись</template>
      <template v-slot:body>Удалить запись?</template>
    </ConfirmModal>
    <div v-for="(todo, index) in todos" :key="index" class="todo-list">
      <div class="todo-list__header">
        <div class="todo-list__name">{{ todo.name }}</div>
        <div class="todo-list__controls">
          <div
            @click="$router.push({ name: 'note', params: { noteId: todo.id } })"
          >
            <Icon
              :name="icons.pencil"
              title="edit"
              color="gray"
              hover-color="forestgreen"
            />
          </div>
          <div @click="remove(index)">
            <Icon
              :name="icons.trash"
              title="delete"
              color="gray"
              hover-color="red"
            />
          </div>
        </div>
      </div>
      <ul class="todo-list__list">
        <li v-for="(item, index) in todo.todos" :key="index" class="list__item">
          <Checkbox disabled :label="item" />
        </li>
        <li v-if="todos.length > 5" class="list__item--more">...</li>
      </ul>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import TODOS from '../todos.json'

import ConfirmModal from '../components/ConfirmModal'
import Checkbox from '../components/Checkbox'
import Icon from '../components/Icon'

import { mdiPencil, mdiDelete } from '@mdi/js'

export default {
  name: 'Home',
  components: {
    ConfirmModal,
    Checkbox,
    Icon
  },
  data() {
    return {
      todos: TODOS,
      icons: {
        pencil: mdiPencil,
        trash: mdiDelete
      },
      showModal: false,
      removeIndex: null
    }
  },
  mounted() {
    console.log(this.todos)
  },
  methods: {
    confirm() {
      this.todos.splice(this.removeIndex, 1)
      this.showModal = false
    },
    deny() {
      this.showModal = false
    },
    remove(index) {
      this.showModal = true
      this.removeIndex = index
    }
  }
}
</script>

<style lang="scss" scoped>
.home {
  max-width: 1280px;
  margin: auto;
  padding: 20px;
  -webkit-column-count: 4;
  -moz-column-count: 4;
  column-count: 4;
  -moz-column-gap: 10px;
  -webkit-column-gap: 10px;
  column-gap: 10px;
}

.todo-list {
  width: 300px;
  margin-bottom: 20px;
  box-sizing: border-box;
  display: inline-block;
  //max-height: 200px;
  overflow: hidden;
  padding: 20px;
  border: 1px solid black;
  border-radius: 4px;

  &__header {
    display: flex;
  }

  &__name {
    font-weight: bold;
  }

  &__controls {
    width: 60px;
    margin-left: auto;
    display: flex;
    justify-content: space-between;
  }

  &__list,
  .list {
    padding: 0;
    list-style-type: none;

    &__item {
      margin-bottom: 5px;
      text-align: left;
    }

    &__item--more {
      padding-left: 21px;
      font-weight: bold;
    }
  }
}

@media screen and (max-width: 1280px) {
  .home {
    max-width: 998px;
    -webkit-column-count: 3;
    -moz-column-count: 3;
    column-count: 3;
  }
}
@media screen and (max-width: 996px) {
  .home {
    max-width: 640px;
    -webkit-column-count: 2;
    -moz-column-count: 2;
    column-count: 2;
  }
}
@media screen and (max-width: 668px) {
  .home {
    max-width: 320px;
    -webkit-column-count: 1;
    -moz-column-count: 1;
    column-count: 1;
  }
}
</style>
