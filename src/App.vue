<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-app-bar-title>Microsoft OTS Exam</v-app-bar-title>

      <v-spacer></v-spacer>

      <v-btn
        icon
        href="https://github.com/Matthew-The-Developer"
      >
        <v-icon>mdi-github</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container>
        <FrequencyDeletion/>
        <PalindromeSwaps/>
        <EqualPiles/>
        <PositiveNegative/>
        <MaxUnique/>
        <SumToZero/>
        <PartitionEqualArrays/>
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
import MaxUnique from '@/components/MaxUnique.vue';
import SumToZero from '@/components/SumToZero.vue';
import PartitionEqualArrays from '@/components/PartitionEqaulArrays.vue';

export default Vue.extend({
  name: 'App',

  components: {
    FrequencyDeletion,
    PalindromeSwaps,
    EqualPiles,
    PositiveNegative,
    MaxUnique,
    SumToZero,
    PartitionEqualArrays,
  },
});
</script>
