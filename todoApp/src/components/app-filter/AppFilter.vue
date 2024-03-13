<template>
  <div class="btn-group">
    <button
      v-for="btn in filterButton"
      :key="btn.filterType"
      class="btn"
      :class="[filterName === btn.filterType ? 'btn-dark' : 'btn-outline-dark']"
      @click="filterHandler(btn.filterType)"
    >
      {{ btn.title }}
    </button>
  </div>
</template>

<script>
export default {
  props: {
    updateFilterHandler: {
      type: Function,
      required: true,
    },
    filterName: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      filterButton: [
        { title: "Barcha kinolar", filterType: "all" },
        { title: "Mashhur kinolar", filterType: "popular" },
        { title: "Eng ko'p ko'rilgan kinolar", filterType: "mostViewers" },
      ],
      filter: "all",
    };
  },
  methods: {
    filterHandler(filter) {
      this.filter = filter;
      this.updateFilterHandler(this.filter);
    },
  },
};
</script>

<style></style>
