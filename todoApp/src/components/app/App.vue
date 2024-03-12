<template>
  <div class="app">
    <div class="content">
      <AppInfo
        :allMoviesCount="movies.length"
        :favouriteMoviesCount="viewersCount()"
      />
      <div class="search-panel">
        <SearchPanel :changeTermHandler="changeTermHandler" />
        <AppFilter
          :updateFilterHandler="updateFilterHandler"
          :filterName="filter"
        />
      </div>
      <MovieList
        :movies="onFilterHandler(searchMovie(movies, term), filter)"
        @onToggle="onToggleHandler"
        @onDelete="onDeleteHandler"
      />
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
      term: "",
      filter: "popular",
    };
  },
  methods: {
    addMovie(movie) {
      this.movies.push(movie);
    },
    onToggleHandler({ id, status }) {
      this.movies = this.movies.map((movie) => {
        if (movie.id === id) {
          console.log({ ...movie, [status]: !movie[status] });

          return { ...movie, [status]: !movie[status] };
        }
        return movie;
      });
    },

    onDeleteHandler(id) {
      this.movies = this.movies.filter((movie) => movie.id != id);
    },

    searchMovie(movies, term) {
      if (term.length == 0) {
        return movies;
      }

      return movies.filter(
        (movie) => movie.name.toLowerCase().indexOf(term) > -1
      );
    },

    changeTermHandler(term) {
      this.term = term;
    },

    viewersCount() {
      return this.movies.filter((movie) => movie.favourite).length;
    },

    onFilterHandler(movies, filter) {
      switch (filter) {
        case "popular":
          return movies.filter((movie) => movie.like);
        case "mostViewers":
          return movies.filter((movie) => movie.viewers > 500);
        default:
          return movies;
      }
    },

    updateFilterHandler(filter) {
      this.filter = filter;
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
