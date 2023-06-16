<script>
  import DateField from './components/DateField.vue';

  export default {
    name: 'App',
    components: {
      DateField,
    }
  }

</script>

<template>
  <main class="main">
    <DateField />
  </main>
</template>

<style lang="scss" scoped>
  @use './assets/scss/utilities' as *;

  .main {
    padding: clampf(16, 780, 32);
  }
</style>
