<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand>Avant</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-navbar-nav>
          <b-nav-item>
            <router-link to="/" class="text-decoration-none text-dark font-weight-bold">Главная</router-link>
          </b-nav-item>
          <b-nav-item>
            <router-link to="/about" class="text-decoration-none text-dark font-weight-bold">О странице</router-link>
          </b-nav-item>
          <b-nav-item>
            <router-link to="/contractors" class="text-decoration-none text-dark font-weight-bold">Контрагенты</router-link>
          </b-nav-item>
        </b-navbar-nav>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "NavMenu",
};
</script>