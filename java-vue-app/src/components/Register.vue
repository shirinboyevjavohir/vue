<template>
  <main class="form-signin w-25 m-auto mt-5">
    <form>
      <h1 class="h3 mb-3 fw-normal">Register</h1>

      <Input :label="'Name'" :type="'text'" />
      <Input :label="'Email address'" :type="'email'" />
      <Input :label="'Password'" :type="'password'" />

      <Button>Register</Button>
    </form>
  </main>
</template>

<script>
export default {};
</script>

<style></style>
