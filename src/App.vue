<template lang="pug">
  .app
    img( src="./assets/logo.png")
    HelloWorld

    button.btn(@click="showPopup") Open popup

    VPopup(
      v-show="isPopupOpen"
      @close="isPopupOpen = false"
    )
      template(slot="filter")
        VFilter(
          v-model="currentFilter"
          :filters="filters"
          label="Filter by:"
        )

      VFavList(
        v-if="isFavorites"
        :items="favoritesList"
        :favorites="favorites"
        @favoriteChange="favoriteChange"
      )
      .albums(v-else)
        VAlbumList(
          v-for="item in items" :key="item.label"
          :label="item.label"
          :items="item.list"
          :favorites="favorites"
          @favoriteChange="favoriteChange"
        )

</template>

<script>
import axios from 'axios';
import HelloWorld from './components/HelloWorld';
import VPopup from './components/VPopup';
import VAlbumList from '@/components/VAlbumList';
import VFavList from '@/components/VFavList';
import VFilter from '@/components/VFilter.vue';

const sortByName = (a, b) => {
  const a1 = a.label;
  const b1 = b.label;
  return a1 > b1
    ? 1
    : a1 < b1
      ? -1
      : 0;
}

export default {
  name: 'App',
  components: {
    HelloWorld,
    VPopup,
    VFilter,
    VAlbumList,
    VFavList
  },
  data() {
    return {
      isPopupOpen: false,
      currentFilter: "A-Z",
      filters: ["A-Z", "Favorites"],
      favorites: [],
      list: [],
      items: {}
    }
  },
  computed: {
    isFavorites() {
      return this.currentFilter === "Favorites"
    },
    favoritesList() {
      return this.list.filter(item => {
        return this.favorites.includes(item.id);
      })
    }
  },
  methods: {
    showPopup() {
      this.isPopupOpen = true;
    },
    favoriteChange(id) {
      if(this.favorites.includes(id)) {
        this.favorites = this.favorites.filter(val => val !== id);
      } else {
        this.favorites.push(id);
      }

      window.localStorage.setItem('favorites', this.favorites);
    }
  },
  async mounted() {
    const {data} = await axios.get('https://jsonplaceholder.typicode.com/photos');

    let items = data.map(item => {
      const {albumId} = item;
      delete item.albumId;
      item.id = `${albumId}_${item.id}`;
      return item;
    }).reduce((res, item) => {
      const key = item.title.charAt(0);
      if (key in res) {
        res[key].list.push(item);
      } else {
        res[key] = {
          label: key,
          list: [item]
        }
      }
      return res;
    }, {})

    this.items = Object.values(items).sort(sortByName);
    this.list = data;

    this.favorites = window.localStorage.getItem('favorites').split(',') || [];
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.app {
  font-family: 'Open Sans', 'Avenir', Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 19px;
  color: #1C214C;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}

.btn {
  background-color: #42b983;
  border: none;
  color: #fff;
  padding: 0.5em 1em;
  font-weight: bold;
  text-transform: uppercase;
}

.albums {
  overflow: hidden;
  display: flex;
  flex-wrap: wrap;
  align-items: flex-start;
  justify-content: space-between;
  justify-content: flex-start;
  margin-right: -40px;
}
</style>
