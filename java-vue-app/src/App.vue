<template>
  <div>
    <div class="container">
      <Navbar />
    </div>
    <RouterView />
  </div>
</template>

<script>
import { Navbar } from "@/components";
import { RouterView } from "vue-router";

export default {
  components: {
    Navbar,
  },
};
</script>

<style></style>
