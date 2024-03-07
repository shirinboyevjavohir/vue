<template>
  <div class="app">
    <div class="content">
      <AppInfo
        :favouriteMoviesCount="movies.filter((c) => c.favourite).length"
        :allMoviesCount="movies.length"
      />
      <div class="search-panel">
        <SearchPanel />
        <AppFilter />
      </div>
      <MovieList :movies="movies" />
      <MovieAddForm @CREATE="addMovie" />
    </div>
  </div>
</template>

<script>
import AppInfo from "../app-info/AppInfo.vue";
import SearchPanel from "../search-panel/SearchPanel.vue";
import AppFilter from "../app-filter/AppFilter.vue";
import MovieList from "../movie-list/MovieList.vue";
import MovieAddForm from "../movie-add-form/MovieAddForm.vue";
export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,
  },
  data() {
    return {
      movies: [
        {
          id: 1,
          name: "Avatar Ang",
          viewers: 234,
          favourite: false,
          like: true,
        },
        { id: 2, name: "Omar", viewers: 867, favourite: true, like: false },
        {
          id: 3,
          name: "Empire of osman",
          viewers: 733,
          favourite: false,
          like: true,
        },
      ],
    };
  },
  methods: {
    addMovie(movie) {
      this.movies.push(movie);
    },
  },
};
</script>

<style>
.app {
  height: 100vh;
  color: #000;
}

.content {
  width: 80%;
  min-height: 700px;
  background: #fff;
  padding: 5rem 0;
  margin: 0 auto;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
