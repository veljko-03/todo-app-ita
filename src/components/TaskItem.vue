<template>
  <div class="todo-item">
    <div class="task-info">
      <h2>{{ task.title }}</h2>

      <p>
        <strong>Priority:</strong>
        {{ task.priority }}
      </p>

      <p>
        <strong>Status:</strong>
        {{ task.completed ? 'Completed' : 'Not completed' }}
      </p>
    </div>

    <div class="task-actions">
      <button>Mark as completed</button>

      <button class="delete-button">Delete</button>
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

.task-info h2 {
  margin: 0 0 10px;
}

.task-info p {
  margin: 5px 0;
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
