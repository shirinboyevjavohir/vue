<template>
  <div>
    Home page {{ counter }}
    <div class="w-25">
      <Button @click="incrementHandler">Increase</Button>
    </div>
    <div class="w-25">
      <Button @click="decrementtHandler">Decrement</Button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    incrementHandler() {
      this.$store.commit("increment");
    },
    decrementtHandler() {
      this.$store.commit("decrement");
    },
  },
  computed: {
    counter() {
      return this.$store.state.count;
    },
  },
};
</script>

<style></style>
