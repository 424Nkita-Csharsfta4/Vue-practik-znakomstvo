<template>
  <form @submit.prevent="searchItunes(searchText)">
  <input type="text" v-model="searchText"/>
  <div v-if="data.results">
  <button @click="searchItunes(searchText)">Поиск музла</button>
  <div v-if="album in data.results" :key="album.artistId">
     <h3>
      Название альбома {{album.collectionName}}</h3>
     <h5>
      Atwork
     </h5>
     <img src="" alt="">
     <h5>
      Цена:
     </h5>
  </div>
  </div>
  </form>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from "vue";
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
export default defineComponent({
  name: "App",
  components: {
    TheShowAlbum
  },
  setup() {
    let albums = reactive<{ data: ItunesTypes }>({ data: {} });
    let searchText = ref("");
    const searchItunes = async (search: string): Promise<void> => {
      const value = await itunesSearch(search);
      albums.data = value;
      console.log("data", albums);
    };
    return { searchItunes, ...toRefs(albums), searchText };
  }
});
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
