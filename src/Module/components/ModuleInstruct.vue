<template>
<!--  TODO: make the inputs into actual components -->
  <v-container class="module-instruct">
    <div class="module-instruct__container">
      <h3 class="mb-3">Instructions</h3>
      <v-textarea
          solo auto-grow
          color="black"
          flat
          outlined
          :disabled = readonly
          rows="3"
          name="input-7-4"
          v-model="k1Collection.instruction"
        ></v-textarea>
        <div v-for="(step,i) in k1Collection.steps" :key="i">
        <v-responsive
        v-if="!readonly"
      class="order text-center grey lighten-2 rounded-circle
      d-inline-flex align-center justify-left mb-3"
      height="40"
      width="40"
    >
      {{ step.rank }}
    </v-responsive>
        <v-textarea
          color="black"
          class="text"
          solo auto-grow
          :disabled = readonly
          flat
          outlined
          name="input-7-4"
          v-model="step.name"
          rows="1"
        ></v-textarea>
        </div>
<v-btn @click="addInstruct" v-if="!readonly"
        depressed outlined width="425px"><v-icon>add</v-icon></v-btn>
        <v-flex v-if="!readonly" style="margin-top: 120px">
        <v-btn depressed outlined height="40px"
        width="200px" class="mr-6"><h3>Discard</h3></v-btn>
        <span><v-btn depressed outlined height="40px" width="200px"
        @click="save()"><h3>Save</h3></v-btn></span>
        </v-flex>
    </div>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue';
import gql from 'graphql-tag';

export default Vue.extend({
  name: 'ModuleInstruct',
  props: {
    readonly: {
      type: Boolean,
      default: false,
    },
  },
  apollo: {
    k1Collection: gql`
      query {
        k1Collection {
          instruction
number
steps {
name
rank
},
  },
}`,
  },
  data: () => ({

  }),
  methods: {
    addInstruct() {
      this.k1Collection.number += 1;
      const k1Collection = { name: '', rank: this.k1Collection.number };
      this.k1Collection.steps.push(k1Collection);
      console.log(this.k1Collection.steps);
    },
    async save() {
      // Call to the graphql mutation
      await this.$apollo.mutate({
      // Query
        mutation: gql`mutation ($instruction: String!, $number: Int!, $steps: [K1CollectionStepUpdateInput]) {
        updateOneK1Collection(set: { instruction: $instruction, number: $number, steps: $steps  }) {
          instruction
          steps{
            rank, 
            name
          }
          number
        }
      }`,
        // Parameters
        variables: {
          instruction: this.k1Collection.instruction,
          steps: this.k1Collection.steps,
          number: this.k1Collection.number,
        },
      });
    },
  },
});
</script>
<style scoped>
  .order{
    position: absolute;
    left: 29%;
  }
  v-textarea{
    position: relative;
  }
</style>
