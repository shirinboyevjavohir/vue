<template>
  <main class="form-signin w-25 m-auto mt-5">
    <form>
      <h1 class="h3 mb-3 fw-normal">Login</h1>

      <Input :label="'Email address'" :type="'email'" />
      <Input :label="'Password'" :type="'password'" />

      <Button>Login</Button>
    </form>
  </main>
</template>

<script>
export default {};
</script>

<style></style>
