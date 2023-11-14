<template>
    <section>
        <h2>{{ title }}</h2>
        <ul>
            <JCard
                v-for="item in visibleList"
                :key="item.id"
                :title="item.title"
                :state="item.state"
                @move="onMove(item.id)"
            >
                {{  item.desc }}
            </JCard>
        </ul>
    </section>
</template>

<script setup>
    import JCard from '@/components/JCard.vue';

    import { defineProps, defineEmits, computed } from 'vue';
    import { string, array } from 'vue-types';

    const props = defineProps({
        title: string(),
        items: array()
    })
    const emits = defineEmits(['goNext'])

    const visibleList = computed(() => props.items)

    const onMove = (id) => {
        emits('goNext', id)
    }

</script>

<style scoped>
    section {
        padding: 12px;
        margin-bottom: 6px;
        border-radius: 8px;
        background-color: var(--color-background-mute);
    }
</style>