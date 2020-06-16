<template>
  <nav>
    <div class="logo">
      <router-link active-class="none" to="/">
        Medicine&reg;
        <small>by P.Greber</small>
      </router-link>
    </div>

    <ul class="nav-links" :class="{'nav-active': active }">
      <li
        @click="active = false"
        :class="{'animated': active, 'route-link-actived': $route.name === 'Order'}"
      >
        <router-link to="/order">Zlecenie leków</router-link>
      </li>
      <li
        @click="active = false"
        :class="{'animated': active, 'route-link-actived': $route.name === 'Contact'}"
      >
        <router-link to="/contact">Kontakt</router-link>
      </li>
    </ul>

    <div class="burger" @click="active = !active">
      <div class="line1"></div>
      <div class="line2"></div>
      <div class="line3"></div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      active: false
    };
  },
  computed: {
    isProjectTypeRoute() {
      return this.$route.matched.some(route => route.name === "Project Type");
    }
  }
};
</script>

<style lang="scss">
nav {
  display: flex;
  justify-content: space-around;
  align-items: center;
  min-height: 8vh;
  background-color: #7396b8;
  z-index: 2;

}

.logo {
  text-transform: uppercase;
  letter-spacing: 5px;
  font-size: 20px;
}

.logo a {
  text-decoration: none;
  color: white;
}

.nav-links {
  display: flex;
  justify-content: space-around;
  width: 40%;
  z-index: 2;
}

.nav-links li {
  list-style: none;
}

.nav-links a {
  color: white;
  text-decoration: none;
  letter-spacing: 2px;
  font-size: 13px;
}

.route-link-actived {
  font-weight: bold;
  color: wheat;
}

.burger {
  display: none;
  cursor: pointer;
}

.burger div {
  width: 25px;
  height: 3px;
  background-color: white;
  margin: 5px;
}

@media screen and (max-width: 1024px) {
  body {
    overflow-x: hidden;
  }

  .nav-links {
    position: absolute;
    right: 0px;
    height: 92vh;
    top: 8vh;
    background-color: #7396b8;
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 40%;
    transform: translateX(100%);
    transition: transform 0.5s ease-in;
  }

  .nav-links li {
    opacity: 0;
  }

  .burger {
    display: block;
  }
}

.nav-active {
  transform: translateX(0%);
}

.animated {
  animation: navLinkFade 0.5s ease forwards 0.6s;
}

@keyframes navLinkFade {
  from {
    opacity: 0;
    transform: translateX(50px);
  }
  to {
    opacity: 1;
    transform: translateX(0px);
  }
}
</style>