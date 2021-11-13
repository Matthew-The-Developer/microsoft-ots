<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-app-bar-title>Microsoft OTS Exam</v-app-bar-title>
    </v-app-bar>

    <v-main>
      <v-container>
        <FrequencyDeletion/>
        <PalindromeSwaps/>
        <EqualPiles/>
        <PositiveNegative/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import FrequencyDeletion from '@/components/FrequencyDeletion.vue';
import PalindromeSwaps from '@/components/PalindromeSwaps.vue';
import EqualPiles from '@/components/EqualPiles.vue';
import PositiveNegative from '@/components/PositiveNegative.vue';

export default Vue.extend({
  name: 'App',

  components: {
    FrequencyDeletion,
    PalindromeSwaps,
    EqualPiles,
    PositiveNegative,
  },

  data: () => ({
    //
  }),
});
</script>
