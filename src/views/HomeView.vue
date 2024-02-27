<template>
  <MovieDetail v-if="selected" v-on:close="selected = null" v-bind:movieId="selected" />
   <MovieList v-on:open="receiveEmit" />
</template>

<script>
import MovieDetail from '@/components/MovieDetail.vue';
import MovieList from '@/components/MovieList.vue';


export default {
    name: 'HomeView',
    components: { MovieList, MovieDetail },
    methods: {
      receiveEmit(filmId) {
        this.selected = filmId; 
      }
    },
  data() {
    return {
      selected: null
    }
  }
}

</script>
