<template>
  <v-app>
    <v-main>
      <FormWizard></FormWizard>
    </v-main>
  </v-app>
</template>

<script>
import FormWizard from './components/FormWizard';

export default {
  name: 'App',

  components: {
    FormWizard,
  },

  data: () => ({
    //
  }),
};
</script>
<style lang="scss">
@import "@/assets/scss/basic.css"
</style>