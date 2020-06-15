<template>
  <svg
    class="icon"
    style="width:18px;height:18px"
    viewBox="0 0 24 24"
    :fill="fill"
    @mouseover="isHover = true"
    @mouseout="isHover = false"
  >
    <title>{{ title }}</title>
    <path :d="path" />
  </svg>
</template>

<script>
export default {
  name: 'Icon',
  props: {
    name: {
      type: String,
      default: ''
    },
    title: {
      type: String,
      default: ''
    },
    color: {
      type: String,
      default: 'currentColor'
    },
    hoverColor: {
      type: String,
      default: 'currentColor'
    }
  },
  data() {
    return {
      isHover: false
    }
  },
  computed: {
    path() {
      return this.name
    },
    fill() {
      return this.isHover ? this.hoverColor : this.color
    }
  }
}
</script>
<style lang="scss" scoped>
.icon {
  cursor: pointer;
}
</style>
