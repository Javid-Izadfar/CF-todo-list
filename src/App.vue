<template>
  <div>
    <JList 
      v-for="list in board"
      :key="list.state"
      :title="list.title"
      :items="list.items"
      @goNext="goToNextState"
    />
  </div>
</template>

<script setup>
  import JList from '@/components/JList.vue'
  import { BOARD_LISTS } from '@/scripts/board.js'

  import { computed, ref } from 'vue'
  import { nanoid } from 'nanoid'
  import { groupBy } from 'lodash'

  const list = ref([
    {
      id: nanoid(),
      title: 'Who knows what?',
      desc: '',
      state: 'backlog'
    },
    {
      id: nanoid(),
      title: 'Make it pretty',
      desc: '',
      state: 'backlog'
    },
    {
      id: nanoid(),
      title: 'Make a better one',
      desc: 'A simple list should be fine!',
      state: 'doing'
    },
    {
      id: nanoid(),
      title: 'Make a todo list',
      desc: 'A simple list should be fine!',
      state: 'done'
    },
  ])

  const board = computed(() => {
    const lists = groupBy(list.value, 'state')
    return BOARD_LISTS.map((item) => ({
      ...item,
      items: lists[item.state]
    }))
  })

  const goToNextState = (id) => {
    const taskIndex = list.value.findIndex(item => item.id === id)
    const listIndex = BOARD_LISTS.findIndex(l => l.state === list.value[taskIndex]?.state)
    
    if (listIndex > -1) {
      const nextState = BOARD_LISTS[listIndex + 1].state
      list.value[taskIndex].state = nextState
    }
  }

</script>

<style scoped>
  .bg-red {
    background: red;
  }
</style>
