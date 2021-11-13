<template>
  <v-card
    class="mx-auto my-4"
    outlined
  >
    <v-card-title>Minimum Deletions to Make Character Frequencies Unique</v-card-title>

    <v-card-text>
      <div class="text--primary mb-6">
        A string <code>s</code> is called <b>good</b> if there are no two different characters in <code>s</code> that have the same <b>frequency</b>.<br>
        Given a string <code>s</code>, return the <b>minimum</b> number of characters you need to delete to make <code>s</code> <b>good</b>.
      </div>

      <div class="d-flex">
        <v-text-field
          v-model="input"
          label="String s"
          filled
          rounded
          dense
          class="shrink"
        ></v-text-field>
      </div>

      <h3>Output: {{ minDeletion(input) }}</h3>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'FrequencyDeletion',

  data: () => ({
    input: '',
  }),

  methods: {
    minDeletion(input: string): number {
      // go through the string and count the frequency of all chars
      let counts = new Map<string, number>();
      [...input].forEach(c => {
        if (counts.has(c)) {
          counts.set(c, (counts.get(c) as number) + 1);
        } else {
          counts.set(c, 1);
        }
      });
      // sort the counts into descending order
      counts = new Map([ ...counts.entries() ].sort((a, b) => b[1] - a[1]));
      // get the maximum frequency
      let max: number = counts.values().next().value;
      let deletes = 0;
      counts.forEach((frequency: number) => {
        // if this frequency is greater than the current maximum
        if (frequency > max) {
          if (max > 0) {
            deletes += (frequency - max);
          } else {
            deletes += frequency;
          }
        }
        // determine the next largest frequency
        max = Math.min(max - 1, frequency - 1);
      });
      return deletes;
    }
  }
});
</script>

<style>

</style>