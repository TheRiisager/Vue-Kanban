<template>
    <v-sheet
        min-height="10rem" 
        color="red-lighten-5"
        width="20rem"
        class="sheet"
        rounded="lg"
        >
        <h3>{{ props.data.title }}</h3>
        <v-divider 
            class="divider"
            thickness="2"
        ></v-divider>
        <v-fab
            extended
            text="+ Add card"
            density="comfortable"
            @click="dialogActive = true"
        ></v-fab>
        <CreateDialog
          :add-fn="addCard"
          :close-fn="closeDialog"
          :active="dialogActive"
          absolute
          max-width="50rem"
        ></CreateDialog>
        <div class="list">
            <draggable
                v-model="items"
                group="items"
                @start="drag=true"
                @end="drag=false"
                >
                <template #item="{element, index}">
                    <Card :key="index" :item="element"></Card>
                </template>
            </draggable>
        </div>
    </v-sheet>
</template>

<script setup lang="ts">
import { Ref, ref } from 'vue';
import Item from '../models/Item';
import draggable from 'vuedraggable';
import CreateDialog from './CreateDialog.vue';
import Column from '@/models/Column';

    const props = defineProps<{
        data: Column
    }>()

    const items: Ref<Item[]> = ref(props.data.cards);
    const dialogActive = ref(false);

    const addCard = (card: Item) => {
        items.value.unshift(card);
        dialogActive.value = false;
    }

    const closeDialog = () => {
        dialogActive.value = false;
    }
</script>

<style>
    .sheet {
        margin: 1rem;
        padding: 1rem;
    }
    .list {
        margin-top: 2rem;
        margin-bottom: 1rem;
    }
    .divider {
        margin-top: 0.5rem;
        margin-bottom: 0.5rem;
    }
</style>