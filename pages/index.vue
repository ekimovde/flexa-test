<template>
  <div class="main">
    <div class="main__wrapper container">
      <div class="main__filter">
        <h4 class="main__title">Фильтр поиска</h4>

        <div class="main__block">
          <ApolloMutation
            :mutation="require('../graphql/getJob.gql')"
            :variables="{ input }"
            @done="onDone"
          >
            <template v-slot="{ mutate }">
              <form class="main__form" v-on:submit.prevent="mutate()">
                <input type="text" class="main__input" v-model="input" />

                <div class="main__button">
                  <button class="main__btn" @click="mutate()">Найти!</button>
                </div>
              </form>
            </template>
          </ApolloMutation>
        </div>
      </div>

      <div class="main__offer">
        <div class="main__block">
          <h4 class="main__title">Информация</h4>

          <CommonsProfileCard
            title="ТЗ по проверке знаний Vue Js и Graphql"
            descr="Екимов Денис Вительевич, Frontend-developer"
            date="May 30, 2021"
            image="https://images.unsplash.com/photo-1461749280684-dccba630e2f6?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80"
          />
        </div>

        <ApolloQuery :query="require('../graphql/allJobs.gql')">
          <template v-slot="{ result: { loading, error, data } }">
            <div class="main__loader" v-if="!loading && error">
              <i
                class="bx bx-loader-circle bx-spin bx-flip-vertical main__icon"
              ></i>
            </div>

            <div class="main__block" v-if="data && !loading && !error">
              <h4 class="main__title">Вакансии</h4>

              <ul class="main__menu">
                <li class="main__item" v-for="job in data.jobs" :key="job.id">
                  <CommonsJobCard :job="job" />
                </li>
              </ul>
            </div>
          </template>
        </ApolloQuery>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'index',
  data() {
    return {
      input: '',
    }
  },
  methods: {
    onDone() {
      alert('worked')
    },
  },
}
</script>

<style lang="scss" scoped>
.main {
  height: calc(100vh - 40px);

  &__wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  &__filter {
    width: 25%;
    height: calc(100vh - 40px);
    background: #f6f8fa;
    padding: 30px 30px;
  }

  &__offer {
    width: 75%;
    height: calc(100vh - 40px);
    padding: 30px 40px;
    overflow: auto;
  }

  &__form {
    display: flex;
    align-items: center;
    flex-direction: column;
  }

  &__input {
    width: 100%;
    border-radius: 6px;
    padding: 8px 10px;
    background: $grey;
    margin-right: 10px;
    margin-bottom: 10px;
  }

  &__button {
    display: flex;
    justify-content: center;
  }

  &__btn {
    padding: 8px 20px;
    background: $blue;
    color: $white;
    font-size: 14px;
    outline: none;
    border-style: none;
    border-radius: 6px;
    cursor: pointer;

    &:hover {
      background: $blue-dark;
    }
  }

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
  .main {
    &__item {
      width: 32%;
    }
  }
}

@media (min-width: 768px) and (max-width: 991px) {
  .main {
    &__item {
      width: 48%;
    }

    &__filter {
      width: 35%;
    }

    &__offer {
      width: 65%;
    }
  }
}

@media (max-width: 767px) {
  .main {
    &__item {
      width: 45%;
    }

    &__filter {
      width: 100%;
      padding: 30px 30px;
      background: none;
      height: 100% !important;
    }

    &__wrapper {
      flex-direction: column;
    }

    &__offer {
      width: 100%;
      padding: 0px 20px;
    }
  }
}

@media (max-width: 650px) {
  .main {
    &__item {
      width: 85%;
    }

    &__menu {
      justify-content: center;
    }

    &__filter {
      width: 100%;
      padding: 30px 30px;
      background: none;
      height: 100% !important;
    }

    &__wrapper {
      flex-direction: column;
    }

    &__offer {
      width: 100%;
      padding: 0px 20px;
    }
  }
}

@media (max-width: 480px) {
  .main {
    &__item {
      width: 100%;
    }

    &__filter {
      padding: 30px 0px;
    }
  }
}
</style>
