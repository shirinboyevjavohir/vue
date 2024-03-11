<template>
  <input
    type="text"
    class="form-control search-input"
    placeholder="Kinolarni qidirish"
    :value="term"
    @input="changeTermHandler"
  />
</template>

<script>
export default {
  props: {
    changeTermHandler: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      term: "",
    };
  },
  methods: {
    changeTermHandler(e) {
      this.term = e.target.value;
      this.changeTermHandler(this.term);
    },
  },
};
</script>

<style scoped>
.search-input {
  margin: 1.5rem 0;
  padding: 1rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
