<template>
      <div :key="task.id" v-for="task in tasks">
        <TaskVue 
        @toggle-priority="$emit('toggle-priority', task.id, task.priority)" 
        @delete-task="$emit('delete-task', task.id, task.priority)" :task="task" />
      </div>
</template>

<script>
import TaskVue from './Task.vue'

    export default {
        name: "Tasks",
        props: {
            tasks: Array
        },
        components: {
            TaskVue,
        },
        emits: ['delete-task', 'toggle-priority']
    }
</script>