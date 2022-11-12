<template>
  <v-app>
    <Calculator/>
  </v-app>
</template>

<script>
import Calculator from './components/Calculator';

export default {
  name: 'App',

  components: {
    Calculator,
  },

  data: () => ({
    //
  }),
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Space+Mono:wght@700&display=swap');
#app{
  background-color: hsl(185, 41%, 84%);
  font-family: 'Space Mono', monospace;
}
</style>
