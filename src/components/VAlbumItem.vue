<template lang="pug">
  .album-item
    .album-item__content
      .album-item__img
        img(:src="thumbnailUrl" :alt="title")
      .album-item__title {{ title }}
    .album-item__fav(
      @click="toggleFav"
      :class="{'is-active': isFav}"
    )
      IStar


</template>

<script>
  import IStar from '@/components/icons/IStar';

  export default {
    components: {
      IStar,
    },
    props: {
      id: String,
      url: String,
      title: {
        type: String,
        required: true
      },
      thumbnailUrl: {
        type: String,
        required: true
      },
      isFav: {
        type: Boolean,
        default: false
      },
    },
    methods: {
      toggleFav() {
        this.$emit('favoriteChange', this.id)
      }
    },
  }
</script>

<style lang="scss">
.album-item {
  width: 260px;
  height: 40px;
  padding: 4px;
  background: #F7F8F9;
  border-radius: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  &__content {
    display: flex;
    align-items: flex-start;
    text-align: left;
    overflow: hidden;
    max-height: 100%;
  }
  &__img {
    width: 32px;
    height: 32px;
    margin-right: 10px;
    flex-shrink: 0;
    background: #C4C4C4;
    border-radius: 8px;
    img {
      width: 100%;
      max-width: 100%;
      max-height: 100%;
    }
  }

  &__title {
    font-size: 12px;
    line-height: 16px;
    color: #1C214C;
  }
  &__fav {
    cursor: pointer;
    padding: 4px;
    color: #DEDEE6;
    &.is-active {
      color: #3E5EF2;
    }
  }

}
</style>
