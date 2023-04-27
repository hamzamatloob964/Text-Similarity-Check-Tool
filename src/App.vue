<template>
  <v-app>
    <v-main>
      <TextSimilarityCheck/>
    </v-main>
  </v-app>
</template>

<script>
//import HelloWorld from './components/HelloWorld';
import TextSimilarityCheck from './components/TextSimilarityCheck.vue';

export default {
  name: 'App',

  components: {
    TextSimilarityCheck
  },

  data: () => ({
    //
  }),
};
</script>
