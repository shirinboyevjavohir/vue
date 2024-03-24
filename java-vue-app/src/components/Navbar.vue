<template>
  <div
    class="d-flex flex-column flex-md-row align-items-center py-3 mb-4 border-bottom"
  >
    <RouterLink :to="{ name: 'home' }">
      <a
        class="d-flex align-items-center link-body-emphasis text-decoration-none fs-3"
      >
        Java
      </a>
    </RouterLink>

    <nav class="d-inline-flex mt-2 mt-md-0 ms-md-auto">
      <RouterLink
        :to="{ name: 'login' }"
        class="me-3 py-2 link-body-emphasis text-decoration-none"
      >
        Login
      </RouterLink>

      <RouterLink :to="{ name: 'register' }">
        <a class="me-3 py-2 link-body-emphasis text-decoration-none" href="#"
          >Register</a
        >
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
