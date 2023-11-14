<template>
    <li>
        <h2 v-if="title">
            {{ title }}
        </h2>
        <template v-else>
            <slot name="title">
                No Title
            </slot>
        </template>
        <slot>
            <p>No Description</p>
        </slot>
        <div v-if="showNextBtn">
            <button @click="moveToNext">Move to next</button>
        </div>
    </li>
</template>

<script setup>
    import { defineProps, defineEmits, computed } from 'vue';
    import { string } from 'vue-types';

    import { BOARD_LISTS } from '@/scripts/board.js'
    
    const props = defineProps({
        title: string(),
        state: string()
    })
    const emits = defineEmits(['move'])

    const showNextBtn = computed(() => props.state !== BOARD_LISTS[BOARD_LISTS.length - 1].state)

    const moveToNext = () => {
        emits('move')
    }
</script>

<style scoped>
    li {
        padding: 12px;
        margin-bottom: 12px;
        border-radius: 8px;
        background: var(--color-background-mute);
    }
    h2 {
        font-size: 32px;
        margin-bottom: 10px;
    }
</style>