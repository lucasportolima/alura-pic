<template>
  <header>
    <a href="/">
      <img src="@/assets/imgs/logo.png" alt="logo" />
      <span class="logo-text">{{ title ? title : "Alurapic Dogs" }}</span>
    </a>

    <nav>
      <ul>
        <li v-for="navItem in navItems" :key="navItem.name">
          <router-link :to="{ name: navItem.name }">{{
            navItem.title
          }}</router-link>
        </li>
        <li>
          <div class="logout-content" @click="logout()">
            <img src="@/assets/icons/logout-64.png" alt="logout" />
            <router-link :to="{ name: 'Login' }">Logout</router-link>
          </div>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
import { routes } from "@/routes";

export default {
  name: "Header",
  computed: {
    navItems() {
      return routes.filter((route) => route.menuHeader);
    },
  },
  methods: {
    logout() {
      // // Old approach
      // localStorage.removeItem("jwt");
      // this.$router.push({ name: "Login" });

      // New approach using Vuex
      this.$store.commit('SET_USER_LOGGED_OUT')
    },
  },
  data: () => ({
    // navItems: [
    //   { name: "Home", url: "/" },
    //   // { name: "Cadastrar Dogo", url: "/cadastrar-dog" },
    //   { name: "Cadastrar Dogo", url: "/cadastrar-dog" },
    //   { name: "Contact", url: "/contact" },
    // ],
  }),
  //   props: ['title'],
  props: {
    //   title: {
    //       type: String,
    //       required: true
    //   }
    title: String,
  }
};
</script>

<style>
header {
  display: flex;
  align-items: center;
  justify-content: space-around;
  padding: 1rem;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.4);
  font: 700 2.4rem Poppins;
  color: var(--var-default-color);
  margin-bottom: 2rem;
}

header a:first-child {
  display: flex;
  align-items: center;
  justify-content: center;
}

header a:first-child img {
  height: 64px;
  width: 64px;
  object-fit: cover;
}

header a:first-child span.logo-text {
  font: 900 3rem Poppins;
  transform: translateY(10px);
}

header nav ul {
  display: flex;
  align-items: center;
  justify-content: center;
}

header nav ul li {
  padding: 1rem;
  margin-left: 1rem;
  cursor: pointer;
}

header nav ul li .logout-content {
  display: flex;
  align-items: center;
  justify-content: center;
}

header nav ul li .logout-content img {
  height: 3.2rem;
  width: 3.2rem;
  object-fit: contain;
  margin-right: 8px;
}
</style>
