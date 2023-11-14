<template>
  <div>
    <JList title="Backlog" @goNext="goToDoing" :items="backlogItems"/>
    <JList title="Doing" @goNext="goToDone" :items="doingItems"/>
    <JList title="Done" :items="doneItems"/>
  </div>
</template>

<script setup>
  import JList from '@/components/JList.vue'

  import { computed, ref } from 'vue'
  import { nanoid } from 'nanoid'

  const list = ref([
    {
      id: nanoid(),
      title: 'Make a todo list',
      desc: 'A simple list should be fine!',
      state: 'backlog'
    }
  ])

  const backlogItems = computed(() => list.value.filter(item => item.state === 'backlog'))
  const doingItems = computed(() => list.value.filter(item => item.state === 'doing'))
  const doneItems = computed(() => list.value.filter(item => item.state === 'done'))

  const goToDoing = (id) => {
    const index = list.value.findIndex(item => item.id === id)
    
    list.value[index].state = 'doing'
  }

  const goToDone = (id) => {
    const index = list.value.findIndex(item => item.id === id)
    
    list.value[index].state = 'done'
  }

</script>

<style scoped>
  .bg-red {
    background: red;
  }
</style>
