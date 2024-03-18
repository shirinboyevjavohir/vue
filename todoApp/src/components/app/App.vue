<template>
  <div class="app">
    <div class="content">
      <AppInfo
        :allMoviesCount="movies.length"
        :favouriteMoviesCount="viewersCount()"
      />
      <Box>
        <SearchPanel :changeTermHandler="changeTermHandler" />
        <AppFilter
          :updateFilterHandler="updateFilterHandler"
          :filterName="filter"
        />
      </Box>
      <Box v-if="!movies.length && !isLoading">
        <p class="text-center fs-3 text-danger">Kinolar yo'q!</p>
      </Box>
      <Box v-else-if="isLoading" class="loader-container">
        <Loader />
      </Box>
      <MovieList
        v-else
        :movies="onFilterHandler(searchMovie(movies, term), filter)"
        @onToggle="onToggleHandler"
        @onDelete="onDeleteHandler"
      />
      <Box class="pagination-container">
        <nav aria-label="pagination">
          <ul class="pagination pagination-lg">
            <li
              v-for="pageNumber in totalPages"
              :key="pageNumber"
              :class="{ active: pageNumber === page }"
              @click="changePageNumHandler(pageNumber)"
            >
              <span class="page-link">{{ pageNumber }}</span>
            </li>
          </ul>
        </nav>
      </Box>
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
import axios from "axios";
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
      movies: [],
      term: "",
      filter: "all",
      isLoading: false,
      limit: 10,
      page: 1,
      totalPages: 0,
    };
  },
  mounted() {
    this.fatchMovies();
  },
  methods: {
    async addMovie(movie) {
      try {
        const response = await axios.post(
          "https://jsonplaceholder.typicode.com/posts",
          movie
        );
        this.movies.push(response.data);
      } catch (error) {
        console.log(error);
      }
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

    async onDeleteHandler(id) {
      try {
        const response = await axios.delete(
          `https://jsonplaceholder.typicode.com/posts/${id}`
        );
        console.log(response);
        this.movies = this.movies.filter((movie) => movie.id != id);
      } catch (error) {
        console.log(error);
      }
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

    async fatchMovies() {
      try {
        this.isLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts",
          {
            params: {
              _limit: this.limit,
              _page: this.page,
            },
          }
        );

        this.totalPages = Math.ceil(
          response.headers["x-total-count"] / this.limit
        );
        const newData = response.data.map((item) => ({
          id: item.id,
          name: item.title,
          like: false,
          favourite: false,
          viewers: item.id * 10,
        }));
        this.movies = newData;
      } catch (error) {
        console.log(error.message);
      } finally {
        this.isLoading = false;
      }
    },
    changePageNumHandler(pageNumber) {
      this.page = pageNumber;
    },
  },
  watch: {
    page() {
      this.fatchMovies();
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

.loader-container,
.pagination-container {
  display: grid;
  place-items: center;
}
</style>
