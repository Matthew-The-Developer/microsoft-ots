<template>
  <v-card
    class="mx-auto my-6"
    outlined
  >
    <v-card-title>Minimum Deletions to Make Character Frequencies Unique</v-card-title>

    <v-card-text>
      <div class="text--primary mb-6">
        Given a string <code>s</code>, what is the minimum number of <b>adjacent swaps</b> required to convert a <code>s</code> into a palindrome. If not possible, return <code>-1</code>.
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

      <h3>Output: {{ palindroneSwaps(input) }}</h3>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'PalindromeSwaps',

  data: () => ({
    input: '',
  }),

  methods: {
    palindroneSwaps(input: string): number {
      // if there isn't a valid string, can't do it
      if (!input) return -1;

      let swaps = 0;

      if (this.isShuffledPalindrome(input)) {
        let characters = [...input]; 
        let front = 0;
        let back = characters.length - 1;

        // while the front index has not passed the back index
        while(back > front) {
          console.log(characters, front, back);
          // if the current two characters do not match
          if (characters[front] != characters[back]) {
            let found = back;

            // starting from the back,
            // look for the index of the character that matching the front index
            while (found > front && characters[found] != characters[front]) {
              found--;
            }

            // if there is not character that matches the front index
            if (found == front) {
              // then move the odd character forward one
              this.swap(characters, front, front + 1);
              swaps++;
            } else {
              // else the character that matches the front index has been found
              // move found character to the back index
              while (found < back) {
                this.swap(characters, found, found + 1);
                swaps++;
                found++;
              }
              // then shrink window
              front++;
              back--;
            }
          } else {
            // else shrink the window
            front++;
            back--;
          }
        }
        return swaps;
      } else {
        return -1;
      }
    },
    
    swap(characters: string[], a: number, b: number): void {
      let temp = characters[a];
      characters[a] = characters[b];
      characters[b] = temp;
    },

    isShuffledPalindrome(value: string): boolean {
      let counts = new Map<string, number>();
      let odds = 0;
      
      // get the frequency of each char in the string
      [...value].forEach(c => {
        if (counts.has(c)) {
          counts.set(c, (counts.get(c) as number) + 1);
        } else {
          counts.set(c, 1);
        }
      });

      counts.forEach((frequency: number) => {
        // if the frequecy is odd, add to the count
        if (frequency % 2 != 0) {
          odds++;
        }
      });

      // if there is only at most 1 odd frequecy in the string, is it doable
      return odds <= 1
    }
  }
})
</script>

<style>

</style>