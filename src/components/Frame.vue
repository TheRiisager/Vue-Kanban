<template>
  <div class="mainContainer">
    <v-fab 
      icon="mdi-plus"
      @click="dialogActive = true"
    ></v-fab>
    <CreateDialog
      for-column
      :active="dialogActive"
      :add-fn="addColumn"
      :close-fn="closeDialog"
      max-width="50rem"
    ></CreateDialog>
    <v-row
      width="100%" 
      justify="center" 
      class="row flex-nowrap" 
    >
      <ColumnComponent
        v-for="column in columns"
        :data="column"
      ></ColumnComponent>
    </v-row>
  </div>
</template>

<script setup lang="ts">
import Column from '@/models/Column';
import { Ref, ref } from 'vue';
import CreateDialog from './CreateDialog.vue';
import ColumnComponent from './ColumnComponent.vue';

  const columns: Ref<Column[]> = ref([]);
  const dialogActive = ref(false);

  const addColumn = (column: Column) => {
    columns.value.push(column);
    dialogActive.value = false;
  }

  const closeDialog = () => {
    dialogActive.value = false
  }


</script>

<style>
  .mainContainer {
    padding: 2rem;
  }
  .row {
    padding-top: 2%;
  }
</style>