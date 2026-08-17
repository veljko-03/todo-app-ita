<template>
  <div
    class="todo-item"
    :class="{
      completed: task.completed,
      'high-priority': task.priority === 'High',
    }"
  >
    <div class="task-info">
      <h2>{{ task.title }}</h2>

      <p>
        <strong>Priority:</strong>
        {{ task.priority }}
      </p>

      <p v-if="task.completed" class="completed-text">Completed</p>

      <p v-else>Not completed</p>
    </div>

    <div class="task-actions">
      <button v-if="!task.completed" @click="$emit('complete', task.id)">Complete</button>

      <button class="delete-button" @click="$emit('delete', task.id)">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskItem',

  props: {
    task: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f9f9f9;
}

.todo-item.completed {
  background-color: #e8f5e9;
  opacity: 0.7;
}

.todo-item.completed h2 {
  text-decoration: line-through;
}

.todo-item.high-priority {
  border-left: 6px solid #e74c3c;
}

.task-info h2 {
  margin: 0 0 10px;
}

.task-info p {
  margin: 5px 0;
}

.completed-text {
  color: #27ae60;
  font-weight: bold;
}

.task-actions {
  display: flex;
  gap: 10px;
}

button {
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background-color: #42b983;
  color: white;
}

.delete-button {
  background-color: #e74c3c;
}

button:hover {
  opacity: 0.85;
}
</style>
