<template lang="pug">
  .album-list
    .album-list__label(v-if="label") {{ label.toUpperCase() }}
    ul.album-list__items
      li.album-list__item(
        v-for="item in list"
        :key="item.id"
      )
        VAlbumItem(
          v-bind="item"
          :isFav="favorites.includes(item.id)"
          @favoriteChange="$emit('favoriteChange', $event)"
        )

</template>

<script>
  import VAlbumItem from '@/components/VAlbumItem.vue';

  export default {
    components: {
      VAlbumItem,
    },
    props: {
      label: String,
      items: Array,
      favorites: Array
    },
    computed: {
      list() {
        return this.items.slice(0, 10)
      }
    }
  }
</script>

<style lang="scss">
.album-list {
  margin-bottom: 26px;
  max-width: 25%;
  margin-right: 40px;
  &__items {
    list-style: none;
    margin: 0;
    padding: 0;
  }
  &__label {
    padding-left: 20px;
    padding-bottom: 8px;
    text-align: left;
  }
  &__item {
    & + & {
      margin-top: 8px;
    }
  }
}

</style>
