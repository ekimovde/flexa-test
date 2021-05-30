<template>
  <div class="job-card">
    <div class="job-card__top">
      <div class="job-card__info">
        <h6 class="job-card__vacancy">{{ job.title }}</h6>

        <div class="job-card__company">
          <div class="job-card__image">
            <img
              src="https://images.unsplash.com/photo-1461749280684-dccba630e2f6?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80"
              alt=""
              class="job-card__avatar"
              v-if="job.company.logoUrl"
            />

            <img
              src="https://images.unsplash.com/photo-1461749280684-dccba630e2f6?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80"
              alt=""
              class="job-card__avatar"
              v-else
            />
          </div>

          <h6 class="job-card__name">{{ job.company.name }}</h6>
        </div>
      </div>

      <div class="job-card__profile">
        <CommonsStatusJob
          v-for="remote in job.remotes"
          :key="remote.id"
          :remote="remote"
        />
      </div>
    </div>

    <div class="job-card__offer">
      <ul class="job-card__menu">
        <li class="job-card__item" v-for="tag in job.tags" :key="tag.id">
          {{ tag.name }}
        </li>
      </ul>
    </div>

    <div class="job-card__footer">
      <div class="job-card__city">
        <ul class="job-card__menu">
          <li
            class="job-card__item job-card__item_city"
            v-for="city in job.cities"
            :key="city.id"
          >
            {{ city.name }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'JobCard',
  props: {
    job: {
      type: Object,
      default: {},
    },
  },
}
</script>

<style lang="scss" scoped>
.job-card {
  padding: 20px;
  border: 2px solid $grey;
  border-radius: 6px;
  width: 100%;
  height: 200px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  &:hover {
    border-color: $blue;
  }

  &__top {
    display: flex;
    justify-content: space-between;
    margin-bottom: 15px;
  }

  &__vacancy {
    max-width: 110px;
    font-size: 12px;
  }

  &__profile {
    margin-top: 15px;
  }

  &__company {
    margin-top: 5px;
    display: flex;
    align-items: center;
  }

  &__name {
    color: #9ca9b6;
    font-size: 11px;
    font-weight: 400;
    margin-left: 5px;
  }

  &__image {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 20px;
    height: 20px;
  }

  &__avatar {
    width: 100%;
    height: 100%;
    border-radius: 50px;
  }

  &__offer {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  &__menu {
    display: flex;
    align-items: center;
    width: 100%;
    flex-wrap: wrap;
  }

  &__item {
    font-size: 12px;
    font-weight: 500;
    color: $blue;
    margin-right: 5px;
    margin-bottom: 5px;
    cursor: pointer;

    &:hover {
      color: $blue-dark;
    }

    &:last-child {
      margin-right: 0;
    }

    &_city {
      color: $black;
      cursor: initial;
      font-size: 13px;

      &:hover {
        color: $black;
      }
    }
  }

  &__city {
    font-size: 13px;
  }
}
</style>
