<template>
  <div class="main-filter">
    <h4 class="main-filter__title">Фильтр поиска</h4>

    <div class="main-filter__block">
      <form class="main-filter__form" v-on:submit.prevent="getVacancy">
        <div class="main-filter__form-block">
          <p class="main-filter__text">Название Компании</p>

          <input type="text" class="main-filter__input" v-model="companyName" />
        </div>

        <div class="main-filter__form-block">
          <p class="main-filter__text">Название вакансии</p>

          <input type="text" class="main-filter__input" v-model="jobName" />
        </div>

        <div class="main-filter__button">
          <button class="main-filter__btn" type="submit">Найти!</button>
        </div>
      </form>
    </div>

    <div class="main-filter__block">
      <form class="main-filter__form" v-on:submit.prevent="getVacancyFromCity">
        <div class="main-filter__form-block">
          <p class="main-filter__text">Поиск по городу</p>

          <input type="text" class="main-filter__input" v-model="cityName" />
        </div>

        <div class="main-filter__button">
          <button class="main-filter__btn" type="submit">Найти!</button>
        </div>
      </form>
    </div>

    <div class="main-filter__button">
      <button class="main-filter__btn" @click="getAllVacancy">
        Все вакансии
      </button>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'MainFilter',
  data() {
    return {
      companyName: 'Segment',
      jobName: 'Senior Fullstack Engineer Platform',
      cityName: 'Berlin',
    }
  },
  apollo: {
    jobs: gql`
      query getAllJobs {
        jobs {
          id
          title
          company {
            id
            name
            logoUrl
          }
          cities {
            id
            name
          }
          remotes {
            id
            name
            type
          }
          tags {
            id
            name
          }
        }
      }
    `,
    city: {
      query: gql`
        query getCityJob($input: LocationInput!) {
          city(input: $input) {
            id
            name
            jobs {
              id
              title
              remotes {
                id
                name
              }
              company {
                id
                name
                logoUrl
              }
              tags {
                id
                name
              }
            }
          }
        }
      `,
      variables() {
        return {
          input: {
            slug: this.cityName
              .split(' ')
              .map((item) => item.toLowerCase())
              .join('-'),
          },
        }
      },
    },
    job: {
      query: gql`
        query getJob($input: JobInput!) {
          job(input: $input) {
            id
            title
            cities {
              id
              name
            }
            remotes {
              id
              name
            }
            company {
              id
              name
              logoUrl
            }
            tags {
              id
              name
            }
          }
        }
      `,
      variables() {
        return {
          input: {
            companySlug: this.companyName
              .split(' ')
              .map((item) => item.toLowerCase())
              .join('-'),
            jobSlug: this.jobName
              .split(' ')
              .map((item) => item.toLowerCase())
              .join('-'),
          },
        }
      },
    },
  },
  methods: {
    getAllVacancy() {
      this.$emit('getAllVacancy', this.jobs)
    },

    getVacancyFromCity() {
      this.$emit('getVacancyFromCity', this.city.jobs)
      this.cityName = 'Berlin'
    },

    getVacancy() {
      let job = {}
      let temp = { ...this.job }
      job['jobs'] = [{ ...temp }]

      this.$emit('getVacancy', job.jobs)
      this.companyName = 'Segment'
      this.jobName = 'Senior Fullstack Engineer Platform'
    },
  },
}
</script>

<style lang="scss" scoped>
.main-filter {
  &__title {
    margin-bottom: 15px;
  }

  &__block {
    margin-bottom: 20px;

    &:last-child {
      margin-bottom: 0;
    }
  }

  &__form {
    display: flex;
    align-items: flex-start;
    flex-direction: column;
    background: #fff;
    padding: 15px;
    border-radius: 6px;

    &-block {
      width: 100%;
    }
  }

  &__text {
    margin-bottom: 15px;
    font-weight: 600;
    font-size: 13px;
  }

  &__input {
    width: 100%;
    border-radius: 6px;
    padding: 8px 10px;
    background: $grey;
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
}

@media (max-width: 767px) {
  .main-filter {
    &__form {
      border: 2px solid $grey;
      border-radius: 6px;
    }
  }
}
</style>
