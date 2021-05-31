<template>
  <div class="main-list">
    <div class="main-list__block">
      <h4 class="main-list__title">Информация</h4>

      <CommonsProfileCard
        title="ТЗ по проверке знаний Vue Js и GraphQl"
        descr="Екимов Денис Вительевич, Frontend-developer"
        date="May 31, 2021"
        image="https://images.unsplash.com/photo-1461749280684-dccba630e2f6?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80"
      />
    </div>

    <div class="main-list__block">
      <h4 class="main-list__title">Вакансии</h4>

      <ul class="main-list__menu">
        <li class="main-list__item" v-for="job in apolloData" :key="job.id">
          <CommonsJobCard :job="job" />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainList',
  props: {
    apolloData: {
      type: Array,
      default: [],
    },
  },
}
</script>

<style lang="scss" scoped>
.main-list {
  &__block {
    margin-bottom: 20px;

    &:last-child {
      margin-bottom: 0;
    }
  }

  &__title {
    margin-bottom: 15px;
  }

  &__menu {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  &__loader {
    display: flex;
    justify-content: center;
  }

  &__icon {
    font-size: 40px;
    color: $blue;
  }

  &__item {
    width: 24%;
    margin-bottom: 10px;

    &:last-child {
      margin-right: 0;
    }
  }
}

@media (min-width: 992px) and (max-width: 1200px) {
  .main-list {
    &__item {
      width: 32%;
    }
  }
}

@media (min-width: 768px) and (max-width: 991px) {
  .main-list {
    &__item {
      width: 48%;
    }
  }
}

@media (max-width: 767px) {
  .main-list {
    &__item {
      width: 45%;
    }
  }
}

@media (max-width: 650px) {
  .main-list {
    &__item {
      width: 85%;
    }

    &__menu {
      justify-content: center;
    }
  }
}

@media (max-width: 480px) {
  .main-list {
    &__item {
      width: 100%;
    }
  }
}
</style>
