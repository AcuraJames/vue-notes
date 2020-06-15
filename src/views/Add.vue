<template>
  <div class="add">
    <h1>Add new Todo</h1>
    <input class="add__title" type="text" placeholder="enter name" />
    <div class="add__item">
      <input
        v-for="(item, index) in items"
        :key="index"
        ref="item"
        type="text"
        placeholder="make smth..."
        @blur="addNextOnBlur"
        @keyup.enter="addNextOnEnter($event, index)"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Add',
  data() {
    return {
      items: 1
    }
  },
  methods: {
    addNextOnBlur(e) {
      if (e.target.value) {
        this.items++
      }
    },
    addNextOnEnter(e, index) {
      this.$refs.item[index].blur()
    }
  }
}
</script>

<style lang="scss" scoped>
.add__title,
.add__item input {
  width: 300px;
  height: 25px;
}
.add__item {
  margin-top: 30px;

  & input {
    margin: auto;
    margin-bottom: 10px;
    display: block;
  }
}
</style>
