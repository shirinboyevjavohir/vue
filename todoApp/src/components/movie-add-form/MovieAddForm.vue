<template>
  <Box>
    <h3>Yangi kino qo'shish</h3>
    <form action="" class="add-form d-flex">
      <Input
        type="text"
        class="new-movie-label"
        placeholder="Qanday kino?"
        v-model="name"
      />
      <Input
        type="number"
        class="new-movie-label"
        placeholder="Necha marotaba ko'rilgan?"
        v-model="viewers"
      />
      <GenericButton
        @click="addForm"
        class="btn btn-outline-dark"
        type="submit"
      >
        Qo'shish
      </GenericButton>
    </form>
  </Box>
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
      if (!this.name || !this.viewers) return;
      const newMovieItem = {
        id: Date.now(),
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

<style scoped></style>
