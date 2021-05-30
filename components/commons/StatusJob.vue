<template>
  <div class="status-job">
    <p class="status-job__text">{{ remote.name }}</p>
  </div>
</template>

<script>
export default {
  name: 'StatusJob',
  props: {
    remote: {
      type: Object,
      default: {},
    },
  },
}
</script>

<style lang="scss" scoped>
.status-job {
  font-size: 8px;
  color: $green;

  &__text {
    font-size: 10px;
  }
}
</style>
