<template>
  <label class="checkbox">
    <input
      type="checkbox"
      v-model="internalValue"
      :id="inputId"
      :checked="checked"
      :disabled="disabled"
    />
    <span class="checkmark"></span>
    <span :class="{ checked: checked }">
      {{ label }}
    </span>
  </label>
</template>

<script>
export default {
  name: 'Checkbox',
  props: {
    value: {
      type: Boolean,
      default: false
    },
    label: {
      type: [String, Object],
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      checked: false,
      lazyValue: this.value
    }
  },
  computed: {
    inputId() {
      return `input${Math.round(Math.random() * 100000)}`
    },
    internalValue: {
      get() {
        return this.lazyValue
      },
      set(val) {
        this.lazyValue = val
        this.checked = !!val
        this.$emit('input', val)
      }
    }
  },
  watch: {
    value: {
      handler(val) {
        this.lazyValue = val
        this.checked = !!val
      },
      immediate: true
    }
  }
}
</script>

<style scoped lang="scss">
.checkbox {
  display: block;
  position: relative;
  padding-left: 25px;
  cursor: pointer;

  input {
    position: absolute;
    opacity: 0;
    width: 0;
    height: 0;
  }

  .checkmark {
    position: absolute;
    top: 0;
    left: 0;
    height: 16px;
    width: 16px;
    border: 1px solid gray;
  }

  .checked {
    text-decoration: line-through;
    color: gray;
  }
}
.checkbox input:checked ~ .checkmark {
  background-color: #2196f3;
}
.checkmark:after {
  content: '';
  position: absolute;
  display: none;
}
.checkbox input:checked ~ .checkmark:after {
  display: block;
}
.checkbox .checkmark:after {
  left: 5px;
  top: 1px;
  width: 4px;
  height: 9px;
  border: solid white;
  border-width: 0 2px 2px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
