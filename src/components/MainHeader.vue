<template>
    <header class="header">
    <div></div>
    <RouterLink to="/">
        <h1>Rick And Morty Database</h1>
    </RouterLink>
    <ul class="header-links">
        <RouterLink to="/">Characters</RouterLink>
        <RouterLink to="/episodes">Episodes</RouterLink>
    </ul>
  </header>
</template>

<script>
export default {
    name: 'MainHeader',
}
</script>

<style scoped>

.header {
  background-color: #333;
  color: #fff;
  padding: 20px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header-links {
  display: flex;
  gap: 20px;
}

</style>