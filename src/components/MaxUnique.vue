<template>
  <v-card
    class="mx-auto my-6"
    outlined
  >
    <v-card-title>Maximum Length of a Concatenated String with Unique Characters</v-card-title>

    <v-card-text>
      <div class="text--primary mb-6">
        Given an array of strings arr. A string s is formed by the concatenation of a subsequence of arr that has unique characters. 
        Return the maximum possible length of s.
        A subsequence is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.
      </div>
  
      <div class="d-flex">
        <v-combobox
          v-model="input"
          hint="Input characters, then press enter"
          label="Array of String"
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

      <h3>Output: {{ maximumLength(input) }}</h3>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'MaxUnique',

  data: () => ({
    input: [] as string[],
  }),

  methods: {
    maximumLength(input: string[]): number {

      return 0;
    }
  }
})
</script>

<style>

</style>