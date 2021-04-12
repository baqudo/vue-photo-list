<template lang="pug">
  .popup(@click.self="$emit('close')")
    .popup__inner
      .popup__head
        .popup__filter
          slot(name="filter")
        button.popup__close(@click="$emit('close')")
          IClose
      .popup__body
        slot
</template>

<script>
import IClose from '@/components/icons/IClose';
export default {
  name: 'VPopup',
  components: {
    IClose
  }
}
</script>

<style lang="scss">
.popup {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(0deg, rgba(37, 39, 55, 0.23), rgba(37, 39, 55, 0.23));

  &__inner {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 1297px;
    max-width: 100%;
    height: 660px;
    padding: 30px 60px 60px;
    background: #FFFFFF;
    border-radius: 12px;
  }

  &__head {
    display: flex;
    justify-content: space-between;
  }

  &__close {
    background: none;
    border: none;
    cursor: pointer;
  }

  &__filter {
    margin-bottom: 1em;
  }

  &__body {
    max-height: 100%;
    overflow-y: auto;
    overflow-x: hidden;
  }
}
</style>
