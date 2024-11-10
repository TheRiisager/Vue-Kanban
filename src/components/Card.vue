<template>
    <v-card
        class="card"
        >
        <v-card-title>
            {{ props.item.title }}
        </v-card-title>
        <v-card-subtitle>
            Created at: {{ props.item.date.toLocaleDateString() }}
        </v-card-subtitle>
        <v-card-text>
            {{ props.item.description }}
        </v-card-text>
    </v-card>
</template>

<script setup lang="ts">
import Item from '@/models/Item';
    const props = defineProps<{
        item: Item
    }>()
</script>

<style>
    .card {
            margin-top: 0.5rem;
            margin-bottom: 0.5rem;
        }
</style>