<template>
  <div class="movie-add-form">
    <h3>Yangi kino qo'shish</h3>
    <form action="" class="add-form d-flex">
      <input
        type="text"
        class="form-control new-movie-label"
        placeholder="Qanday kino?"
        :value="name"
        @input="name = $event.target.value"
      />
      <input
        type="number"
        class="form-control new-movie-label"
        placeholder="Necha marotaba ko'rilgan"
        :value="viewers"
        @input="viewers = $event.target.value"
      />
      <button @click="addForm" class="btn btn-outline-dark" type="submit">
        Qo'shish
      </button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      viewers: "",
    };
  },
  methods: {
    addForm(e) {
      e.preventDefault();
      const newMovieItem = {
        name: this.name,
        viewers: this.viewers,
        favourite: false,
        like: false,
      };

      this.$emit("CREATE", newMovieItem);

      this.name = "";
      this.viewers = "";
    },
  },
};
</script>

<style scoped>
.movie-add-form {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
