<template>
  <div
    class="d-flex flex-column flex-md-row align-items-center py-3 mb-4 border-bottom"
  >
    <RouterLink
      :to="{ name: 'home' }"
      class="d-flex align-items-center link-body-emphasis text-decoration-none fs-3"
    >
      Java
    </RouterLink>

    <nav class="d-inline-flex mt-2 mt-md-0 ms-md-auto">
      <RouterLink
        :to="{ name: 'login' }"
        class="me-3 py-2 link-body-emphasis text-decoration-none"
      >
        Login
      </RouterLink>

      <RouterLink
        :to="{ name: 'register' }"
        class="me-3 py-2 link-body-emphasis text-decoration-none"
      >
        Register
      </RouterLink>
    </nav>
  </div>
</template>

<script>
import { RouterLink } from "vue-router";
export default {
  data() {
    return {};
  },
};
</script>

<style></style>
