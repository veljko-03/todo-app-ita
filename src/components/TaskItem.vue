<template>
  <div
    class="todo-item"
    :class="{
      completed: task.completed,
      'high-priority': task.priority === 'High',
    }"
  >
    <div class="task-content">
      <div class="task-check">
        <div class="status-dot" :class="{ done: task.completed }"></div>
      </div>

      <div class="task-info">
        <h2>{{ task.title }}</h2>

        <div class="task-meta">
          <span class="priority" :class="task.priority.toLowerCase()">
            {{ task.priority }}
          </span>

          <span v-if="task.completed" class="status completed-status"> Completed </span>

          <span v-else class="status"> In progress </span>
        </div>
      </div>
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
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  padding: 20px 22px;
  background: white;
  border: 1px solid #e8ebf1;
  border-radius: 16px;
  box-shadow: 0 5px 20px rgba(31, 41, 55, 0.04);
  transition: 0.2s ease;
}

.todo-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(31, 41, 55, 0.08);
}

.todo-item.high-priority {
  border-left: 4px solid #ef4444;
}

.todo-item.completed {
  background: #fafbfc;
}

.task-content {
  display: flex;
  align-items: center;
  gap: 15px;
  min-width: 0;
}

.task-check {
  flex-shrink: 0;
}

.status-dot {
  width: 12px;
  height: 12px;
  border: 2px solid #cbd2df;
  border-radius: 50%;
}

.status-dot.done {
  border-color: #22c55e;
  background: #22c55e;
}

.task-info {
  min-width: 0;
}

.task-info h2 {
  margin: 0 0 9px;
  color: #172033;
  font-size: 16px;
  font-weight: 600;
}

.completed .task-info h2 {
  color: #929aaa;
  text-decoration: line-through;
}

.task-meta {
  display: flex;
  align-items: center;
  gap: 8px;
}

.priority,
.status {
  display: inline-flex;
  align-items: center;
  padding: 4px 9px;
  border-radius: 20px;
  font-size: 11px;
  font-weight: 600;
}

.priority.high {
  background: #fef2f2;
  color: #dc2626;
}

.priority.medium {
  background: #fff7ed;
  color: #ea580c;
}

.priority.low {
  background: #f0fdf4;
  color: #16a34a;
}

.status {
  background: #f3f4f6;
  color: #6b7280;
}

.completed-status {
  background: #ecfdf5;
  color: #16a34a;
}

.task-actions {
  display: flex;
  gap: 8px;
  flex-shrink: 0;
}

.icon-button {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: 0.2s ease;
}

.icon-button img {
  width: 19px;
  height: 19px;
}

.complete-button {
  background: #ecfdf5;
}

.complete-button:hover {
  background: #d1fae5;
  transform: scale(1.05);
}

.delete-button {
  background: #fef2f2;
}

.delete-button:hover {
  background: #fee2e2;
  transform: scale(1.05);
}

@media (max-width: 500px) {
  .todo-item {
    padding: 16px;
  }

  .task-meta {
    flex-wrap: wrap;
  }

  .task-actions {
    align-self: flex-start;
  }
}
</style>
