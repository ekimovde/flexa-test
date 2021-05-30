<template>
  <div class="navbar">
    <div class="navbar__wrapper container">
      <div class="navbar__brand">
        <h4 class="navbar__title">Flexa</h4>
      </div>

      <ul class="navbar__menu">
        <li class="navbar__item" v-for="(link, index) in links" :key="index">
          <nuxt-link class="navbar__link" :to="link.to">
            <i class="bx bx-home-alt navbar__icon"></i>

            <p class="navbar__text">{{ link.title }}</p>
          </nuxt-link>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Navbar',
  data() {
    return {
      links: [
        {
          title: 'Главная',
          to: '/',
        },
      ],
    }
  },
}
</script>

<style lang="scss" scoped>
.navbar {
  border-bottom: 1px solid #eceef0;
  height: 40px;
  display: flex;
  align-items: center;

  &__wrapper {
    display: flex;
    align-items: center;
  }

  &__brand {
    margin-right: 20px;
  }

  &__icon {
    margin-right: 5px;
    font-size: 20px;
  }

  &__link {
    color: $black;
    position: relative;
    display: flex;
    align-items: center;

    &.nuxt-link-exact-active {
      color: $orange;

      &::after {
        content: '';
        display: block;
        width: 100%;
        height: 1px;
        position: absolute;
        bottom: -10px;
        left: 0;
        background: $orange;
      }
    }
  }

  &__text {
    font-size: 14px;
  }
}
</style>
