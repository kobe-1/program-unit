<template>
  <v-container class="module-metrics">
    <div class="module-metrics__container">
      <template>
        <v-data-table
          :headers="headers"
          :items="milestones"
          :items-per-page="5"
          class="elevation-1"
        ></v-data-table>
</template>
    </div>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue';
import gql from 'graphql-tag';

export default Vue.extend({
  name: 'ModuleMetrics',
  apollo: {
  },
  data: () => ({
    headers: [
      {
        text: 'Milestones',
        align: 'start',
        sortable: false,
        value: 'name',
      },
      { text: 'Average amount of words used', value: 'words' },
    ],
    milestones: [
      {
        name: 'Event X',
        words: 338,
      },
    ],
  }),
});
</script>

<style scoped>
  h3 {
     text-align:justify
  }
</style>
