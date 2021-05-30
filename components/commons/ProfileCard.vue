<template>
  <div class="profile-card">
    <div class="profile-card__top">
      <div class="profile-card__image">
        <img :src="image" alt="" class="profile-card__avatar" />
      </div>

      <div class="profile-card__date">
        <span class="profile-card__date-text"> {{ date }} </span>
      </div>
    </div>

    <div class="profile-card__offer">
      <h2 class="profile-card__title">
        {{ title }}
      </h2>

      <p class="profile-card__descr">
        {{ descr }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProfileCard',
  props: {
    title: {
      type: String,
      required: true,
    },
    descr: {
      type: String,
      required: true,
    },
    date: {
      type: String,
      required: true,
    },
    image: {
      type: String,
      required: true,
    },
  },
}
</script>

<style lang="scss" scoped>
.profile-card {
  background: $blue;
  padding: 20px;
  width: 100%;
  border-radius: 6px;
  color: $white;

  &__top {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  &__image {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 30px;
    height: 30px;
  }

  &__avatar {
    width: 100%;
    height: 100%;
    border-radius: 50px;
  }

  &__date {
    &-text {
      font-size: 12px;
      font-weight: 500;
    }
  }

  &__offer {
    margin-top: 10px;
  }

  &__title {
    color: $white;
  }

  &__descr {
    margin-top: 20px;
    font-size: 14px;
    color: #afe0ff;
  }
}

@media (max-width: 480px) {
  .profile-card {
    &__title {
      font-size: 20px;
    }

    &__descr {
      margin-top: 16px;
    }
  }
}
</style>
