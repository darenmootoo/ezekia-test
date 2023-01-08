<template>
  <div class="navbar">
    <!-- <img src="" alt="" /> -->
    <div class="navbar__logo">
      <font-awesome-icon
        class="navbar__image"
        icon="fa-solid fa-earth-americas"
      />
      <!-- Translated versions would appear here -->
      <h2 class="navbar__title">National History Museum</h2>
    </div>
    <div class="navbar__dropdown">
      <font-awesome-icon
        class="navbar__menu"
        icon="fa-solid fa-bars"
        @click="dropdownActive = !dropdownActive"
      />
      <div class="navbar__dropdown--outer" v-if="dropdownActive">
        <nav class="navbar__dropdown--inner">
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/about">Dinosaurs</RouterLink>
        </nav>
      </div>
    </div>
  </div>
</template>

<script>
// import { RouterLink } from "vue-router";
export default {
  name: "NavBar",
  data() {
    return {
      dropdownActive: false,
    };
  },
};
</script>

<style lang="scss" scoped>
.navbar {
  padding: 1rem;
  background-color: var(--navbar);
  display: flex;
  align-items: center;
  width: 100%;
  justify-content: space-between;

  &__image {
    margin-right: 1rem;
  }

  &__logo {
    display: flex;
    align-items: center;
  }

  &__dropdown {
    position: relative;
    cursor: pointer;

    &--outer {
      position: absolute;
      right: 2rem;
    }

    &--inner {
      display: flex;
      flex-direction: column;
      z-index: 1;
      background: white;
      padding: 10px;
      border-radius: 10px;
    }
  }
}
</style>
