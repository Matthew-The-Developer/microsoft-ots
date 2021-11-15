<template>
  <v-card
    class="mx-auto my-4"
    outlined
  >
    <v-card-title>Can partition array into n subsets of equal totals</v-card-title>

    <v-card-text>
      <div class="text--primary mb-6">
        Given an array of numbers, determine if that array number be divided into n subsets where all subsets have an equal total.
      </div>

      <div class="d-flex">
        <v-text-field
          v-model="devisions"
          :rules="[ partitionLimit ]"
          label="Integer n"
          type="number"
          filled
          rounded
          dense
          class="shrink mr-1"
        ></v-text-field>

        <v-combobox
          v-model="values"
          :rules="[ rules.numeric ]"
          hint="Input number, then press enter"
          label="Array numbers"
          class="shrink ml-1"
          type="number"
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

      <h3>Output: {{ getSubsets(values, devisions) }}</h3>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'PartitionEqualArrays',

  data: () => ({
    values: [] as string[],
    devisions: null,
    rules: {
      numeric: (v: string[]) => {
        for (var i = 0; i < v.length; i++) {
          if(/[^0-9]/g.test(v[i])) {
            return "Insert numbers only";
          }
        }
        return true;
      }
    },
  }),

  methods: {
    getSubsets(values: string[], devisions: number): boolean {
      if (!devisions || values.length < 1 || devisions > values.length) return false;

      const numbers = values.map(value => parseInt(value));
      let sum = numbers.reduce((sum, value) => sum + value, 0);
      
      if (sum % devisions != 0) return false;

      let visited = new Array<boolean>(numbers.length);

      return this.solve(numbers, devisions, 0, sum / devisions, visited, 0);
    },

    solve(
      numbers: number[],
      devisions: number,
      currentSum: number,
      target: number,
      visited: boolean[],
      start: number
    ): boolean {
      if (devisions == 1) return true;
      if (currentSum > target) return false;

      if (currentSum == target) return this.solve(numbers, devisions - 1, 0, target, visited, 0);

      for (let index = start; index < numbers.length; index++) {
        if (!visited[index]) {
          visited[index] = true;
          if (this.solve(numbers, devisions, currentSum + numbers[index], target, visited, index + 1)) {
            return true;
          } else {
            visited[index] = false;
          }
        }
      }
      return false;
    },

    partitionLimit(value = 0) {
      return value <= this.values.length || 'Partitions cannot be greater than values';
    }
  }
})
</script>

<style>

</style>