<template>
    <div 
    v-for="task in tasks"
    :key="task.id">
        <Task 
            @toggle-reminder="$emit('toggle-reminder', task.id)" 
            @delete-task="$emit('delete-task', task.id)" 
            @edit-clicked="$emit('edit-task', task)"
            :task="task" />
    </div>
</template>

<script>
import Task from './Task'
    export default {
        name: 'Tasks',
        props: {
            tasks: Array
        },
        components: {
            Task
        },
        emits: ['delete-task', 'toggle-reminder', 'edit-task']
    }
</script>

<style scoped>

</style>