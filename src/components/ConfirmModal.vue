<template>
  <div class="modal-mask">
    <div class="modal">
      <div class="modal__header">
        <slot name="header"></slot>
      </div>
      <div class="modal__body">
        <slot name="body"></slot>
      </div>
      <div class="modal__footer">
        <slot name="footer">
          <button @click="$emit('confirm')">Yes</button>
          <button @click="$emit('deny')">No</button>
        </slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ConfirmModal'
}
</script>

<style lang="scss">
.modal-mask {
  position: fixed;
  z-index: 998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal {
  width: 300px;
  margin: 0 auto;
  padding: 20px;
  background-color: #fff;
  border-radius: 4px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  z-index: 999;
  position: absolute;
  top: 30%;
  left: calc(50% - 150px);

  &__header {
    margin-top: 0;
    color: #42b983;
  }

  &__body {
    margin: 20px 0;
    padding: 20px;
  }

  &__footer button {
    float: right;
    margin-right: 5px;
  }
}
</style>
