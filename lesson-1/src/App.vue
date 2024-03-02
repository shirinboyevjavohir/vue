<template>
  <div>
    <h1>Counter {{ counter }}</h1>
    <div>
      <button @click="onInc">Add</button>
      <button @click="onDec">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      counter: 0,
    };
  },
  methods: {
    onInc() {
      this.counter += 1;
    },
    onDec() {
      this.counter -= 1;
    },
  },
};
</script>

<style></style>
