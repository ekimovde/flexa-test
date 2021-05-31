<template>
  <div class="main">
    <div class="main__wrapper container">
      <div class="main__filter">
        <MainFilter
          @getVacancy="apolloData = $event"
          @getAllVacancy="apolloData = $event"
          @getVacancyFromCity="apolloData = $event"
        />
      </div>

      <div class="main__offer">
        <MainList :apolloData="apolloData" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'index',
  data() {
    return {
      apolloData: [],
    }
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
}

@media (min-width: 768px) and (max-width: 991px) {
  .main {
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
    &__filter {
      padding: 30px 0px;
    }
  }
}
</style>
