<template>
    <v-dialog
        :model-value="active"
        persistent
    >
        <v-sheet
            rounded="lg"
            class="dialogContent"
        >
            <h3>Add a {{ forColumn ? "column" : "card" }}</h3>
            <v-divider 
                class="divider"
                thickness="2"
            ></v-divider>
            <v-form>
                <v-text-field
                    v-model="title"
                    label="Title"
                >
                </v-text-field>
                <div v-if="!props.forColumn">
                    <v-textarea
                    v-model="description"
                    label="Description"
                    >
                    </v-textarea>
                </div>
                <v-row>
                    <v-btn @click="() => add()">Add</v-btn>
                    <v-btn @click="closeFn">Close</v-btn>
                </v-row>
            </v-form>
        </v-sheet>
    </v-dialog>
</template>

<script lang="ts" setup>
import Column from '@/models/Column';
import Item from '@/models/Item';
import { ref } from 'vue';

    const props = defineProps<{
        addFn: (...args: any[]) => void
        closeFn: () => void
        active: boolean
        forColumn?: boolean
    }>();

    const title = ref("");
    const description = ref("");

    const add = () => {
        if(!props.forColumn) {
            const item: Item = {
                title: title.value,
                description: description.value,
                date: new Date(Date.now())
            }

            props.addFn(item);
        }

        if(props.forColumn) {
            const column: Column = {
                title: title.value,
                cards: []
            }

            props.addFn(column)
        }
        
        title.value = "";
        description.value = "";
    }
</script>

<style>
    .dialogContent {
        padding: 1.5rem;
    }
</style>