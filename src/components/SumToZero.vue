<template>
  <v-card
    class="mx-auto my-6"
    outlined
  >
    <v-card-title>Find N Unique Integers Sum up to Zero</v-card-title>

    <v-card-text>
      <div class="text--primary mb-6">
        Given an integer n, return any array containing n unique integers such that they add up to 0.
      </div>

      <div class="d-flex">
        <v-text-field
          v-model="input"
          label="Integer n"
          type="number"
          filled
          rounded
          dense
          class="shrink"
        ></v-text-field>
      </div>

      <h3>Output: {{ uniqueIntegers(input) }}</h3>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'SumToZero',

  data: () => ({
    input: 0,
  }),

  methods: {
    uniqueIntegers(input: string): number[] {
      if (!input) {
        return [];
      }

      let answer = Array(parseInt(input));
      let sum = 0;
      
      for(let index = 0; index < answer.length; index++) {
        answer[index] = index + 1;
        sum += index + 1;
      }

      answer[answer.length - 1] -= sum;

      return answer;
    }
  }
})
</script>

<style>

</style>