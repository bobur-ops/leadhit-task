<template>
  <nav class="purple darken-3">
    <div class="nav-wrapper">
      <router-link to="/" class="brand-logo">LeadHit</router-link>
      <ul id="nav-mobile" class="right hide-on-med-and-down">
        <router-link tag="li" to="/" exact active-class="active"
          ><a href="sass.html">Авторизация</a></router-link
        >
        <router-link tag="li" to="/analytics" exact active-class="active"
          ><a href="sass.html">Аналитика</a></router-link
        >
      </ul>
    </div>
  </nav>
</template>
<script>
export default {};
</script>
<style lang="scss" scoped>
nav {
  padding: 0 2rem;
}
</style>
