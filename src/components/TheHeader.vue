<template>
  <header class="header">
    <nav class="header__main-nav">
      <div class="header__logo">The Movie DB</div>
      <ul>
        <li>
          <RouterLink to="/">Home</RouterLink>
        </li>
        <li>
          <RouterLink to="/about">About</RouterLink>
        </li>
      </ul>
    </nav>
  </header>
</template>

<style lang="scss" scoped>
.header {
  height: 10rem;
  background: #2c3e50;
  color: white;
  padding: 0 2rem;

  &__logo {
    font-size: 2rem;
    font-weight: 700;
  }

  &__main-nav {
    height: 100%;
    display: flex;
    align-items: center;

    ul {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 1rem;
      height: inherit;
      margin-left: 4rem;
    }

    li:not(:last-child)::after {
      content: '|';
      display: inline-block;
      margin-left: 1rem;
    }

    a {
      font-weight: bold;
      color: white;
      text-decoration: none;
    }

    a.router-link-exact-active {
      color: #42b983;
    }
  }
}

</style>
