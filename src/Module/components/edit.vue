<template>
<v-container class="module-edit">
  <div class="module-edit__container">
    <h3>Entry Question</h3>
    <br>
    <br>
    <v-icon class="sins">edit</v-icon>
    <h3 class="anything">What are some of your next steps after the activity?</h3>
    <br>
  <v-card>
    <v-card-title>
      User
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
        color="black"
      ></v-text-field>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="activity"
      :search="search"
    ></v-data-table>
  </v-card>
  </div>
</v-container>
</template>

<script lang="ts">
import Vue from 'vue';
// import gql from 'graphql-tag';

export default Vue.extend({
  name: 'ModuleEdit',
  apollo: {
  },
  data: () => ({
    search: '',
    headers: [
      {
        text: 'User',
        align: 'start',
        sortable: false,
        value: 'name',
      },
      { text: 'Event X', value: 'x' },
    ],
    activity: [
      {
        name: 'User 1',
        x: 'X',
      },
      {
        name: 'User 2',
        x: 'X',
      },
      {
        name: 'User 3',
        x: 'X',
      },
    ],
  }),
});
</script>

<style scoped>
 h3 {
   text-align:center;
 }
 .anything {
   position: relative;
 }
 .sins {
   position: absolute;
 }
</style>
