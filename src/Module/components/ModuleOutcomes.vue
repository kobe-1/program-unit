<template>
  <v-container class="module-outcomes">
    <div class="module-outcomes__container">
      <h3>Minimum amount of words needed to log entry</h3>
      <br>
      <v-text-field
        class="poopypants centered-input text--darken-3 mt-3"
        v-model ="k1Outcomes[0].words"
        color="grey lighten-43"
        outlined/>
      <br>
      <br>
      <v-flex style="margin-top: 120px; text-align:center;">
        <v-btn depressed outlined height="40px"
        width="200px" class="mr-3"><h3>Discard</h3></v-btn>
        <span><v-btn depressed outlined height="40px" width="200px"
        @click="save()"><h3>Save</h3></v-btn></span>
      </v-flex>
    </div>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue';
// import gql from 'graphql-tag';
import gql from 'graphql-tag';

export default Vue.extend({
  name: 'ModuleOutcomes',
  apollo: {
    k1Outcomes: gql`
      query {
        k1Outcomes {
          words
  },
  }`,
  },
  data: () => ({
    wordcount: '200',
  }),
  methods: {
    async save() {
      await this.$apollo.mutate({
      // Query
        mutation: gql`mutation ($words: Int!) {
        updateOneK1Outcome(set: { words:$words  }) {
          words
        }
      }`,
        // Parameters
        variables: {
          words: this.k1Outcomes[0].words,
        },
      });
    },
  },
});
</script>

<style scoped>
 h3 {
   text-align:center
 }
 .box {
   width: 200px;
   margin-left: 145px;
   text-align:center;
   padding: auto;
 }
  .centered-input >>> input {
    text-align: center;
 }
 .poopypants {
   width: 200px;
   margin-left: 145px;
 }
</style>
