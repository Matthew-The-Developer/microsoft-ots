<template>
  <v-card
    class="mx-auto my-6"
    outlined
  >
    <v-card-title>Largest K such that both K and -K exist in array</v-card-title>

    <v-card-text>
      <div class="text--primary mb-6">
        Given an array A of N integers, returns the lagest integer K > 0 such that both values K and -K exist in array A. 
        If there is no such integer, the function should return 0.
      </div>

      <div class="d-flex">
        <v-combobox
          v-model="input"
          :rules="rules"
          hint="Input number, then press enter"
          label="Array of Numbers"
          class="shrink"
          append-icon=""
          chips
          clearable
          multiple
          filled
          rounded
          dense
        >
          <template v-slot:selection="{ attrs, item, select, selected }">
            <v-chip
              v-bind="attrs"
              :input-value="selected"
              close
              @click="select"
              @click:close="remove(item)"
            >
              {{ item }}
            </v-chip>
          </template>
        </v-combobox>
      </div>

      <h3>Output: {{ largestK(input) }}</h3>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'PositiveNegative',

  data: () => ({
    input: [] as string[],
    rules: [
      function(v: string[]){
        for (var i = 0; i < v.length; i++) {
          if(!(/^-?\d*\.{0,1}\d+$/.test(v[i]))) {
            return "Insert numbers only";
          }
        }
        return true;
      }
    ]
  }),

  methods: {
    largestK(input: string[]): number {
      let values = input.map(value => parseInt(value));
      // there is 1 or number, then there is not inverse
      if (values.length <= 1) return 0;

      // sort negative to positive
      values = values.sort((a, b) => a - b);

      let front = 0;
      let back = values.length - 1;

      while (back > front) {
        if (Math.abs(values[front]) > Math.abs(values[back])) {
          front++;
        } else if (Math.abs(values[front]) < Math.abs(values[back])) {
          back--;
        } else {
          return Math.abs(values[front]);
        }
      }

      return 0;
    },

    remove(item: string) {
      this.input.splice(this.input.indexOf(item), 1);
      this.input = [...this.input];
    },
  }
})
</script>

<style>

</style>