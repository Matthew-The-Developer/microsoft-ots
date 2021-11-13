<template>
  <v-card
    class="mx-auto my-4"
    outlined
  >
    <v-card-title>Minimum Steps to Make Piles Equal Height</v-card-title>

    <v-card-text>
      <div class="text--primary mb-6">
        Given <code>n</code> piles of <b>differing</b> heights, determine the <b>minimum steps</b> needed to remove boxes to <b>equalize all</b> heights.<br>
        In <code>1</code> step, any number of boxes can be removed from the <b>tallest pile</b> to try to equalize it's height with the <b>next tallest</b> pile.
      </div>
      
      <div class="d-flex">
        <v-combobox
          v-model="input"
          :rules="rules"
          hint="For Pile Heights. Input number, then press enter"
          label="Pile Heights"
          class="shrink"
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

      <h3>Output: {{ minSteps(input) }}</h3>
    </v-card-text>

  </v-card>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'EqualPiles',

  data: () => ({
    input: [] as string[],
    rules: [
      function(v: string[]){
        for (var i = 0; i < v.length; i++) {
          if(/[^0-9]/g.test(v[i])) {
            return "Insert numbers only";
          }
        }
        return true;
      }
    ]
  }),

  methods: {
    minSteps(input: string[]): number {
      let piles = input.map(value => parseInt(value));
      // there is 1 or less piles, then no steps needed
      if (piles.length <= 1) return 0;
      // sort piles tallest to shortest
      piles = piles.sort((a, b) => b - a);
      let steps = 0;
      let distinctHeights = 0;
      // starting with the second tallest pile
      // loop through the remaining piles
      for(let index = 1; index < piles.length; ++index) {
        // if the next tallest pile is the same height as the current pile
        if (piles[index] == piles[index - 1]) {
          // then add a step for each distinct height there is
          steps += distinctHeights;
        } else {
          // else the current pile and the next tallest do not match
          // which is a new distinct height
          ++distinctHeights;
          steps += distinctHeights;
        }
      }
      return steps;
    },

    remove(item: string) {
      this.input.splice(this.input.indexOf(item), 1)
      this.input = [...this.input];
    },
  }
})
</script>

<style>

</style>