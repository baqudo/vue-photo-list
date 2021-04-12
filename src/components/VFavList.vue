<template lang="pug">
  .fav-list
    ul.fav-list__items
      li.fav-list__item(
        v-for="item in items"
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
    }
  }
</script>

<style lang="scss">
.fav-list {
  overflow: hidden;
  &__items {
    list-style: none;
    margin: -8px;
    padding: 0;
    display: flex;
    flex-wrap: wrap;
  }
  &__item {
    margin: 8px;
  }
}

</style>
