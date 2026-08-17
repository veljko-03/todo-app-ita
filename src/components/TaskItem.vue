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
      <button
        v-if="!task.completed"
        class="icon-button complete-button"
        @click="$emit('complete', task.id)"
        title="Complete task"
      >
        <img src="/check.svg" alt="Complete" />
      </button>

      <button
        class="icon-button delete-button"
        @click="$emit('delete', task.id)"
        title="Delete task"
      >
        <img src="/trash.svg" alt="Delete" />
      </button>
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

.icon-button {
  width: 42px;
  height: 42px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.icon-button img {
  width: 22px;
  height: 22px;
}

.icon-button:hover {
  opacity: 0.8;
}
</style>
