<template>
    <div 
    @dblclick="$emit('toggle-priority', task.id)"
    :class="[task.priority ? 'priority' : 'noreminder', 'task']" >
        <h3> {{ task.text }} <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i> </h3>
        <p> {{ task.day }} </p>
    </div>
</template>

<script>
    export default {
        name: 'Task',
        props: {
            task: Object
        },
}
</script>

<style scope>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.priority {
  border-left: 5px solid rgb(128, 15, 0);
}

.noreminder {
  border-left: 5px solid rgb(0, 5, 46);
}

.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

p {
  font-family: sans-serif;
}
</style>