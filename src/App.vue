<template>
  <div id="app">
    <h1>To Do App</h1>

    <div class="todo-list">
      <div v-for="task in tasks" :key="task.id" class="todo-item">
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
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  data() {
    return {
      tasks: [
        {
          id: 1,
          title: 'Learn Vue basics',
          completed: true,
          priority: 'High',
        },
        {
          id: 2,
          title: 'Practice Vue directives',
          completed: false,
          priority: 'Medium',
        },
        {
          id: 3,
          title: 'Create To Do App',
          completed: false,
          priority: 'Low',
        },
      ],
    }
  },
}
</script>

<style>
#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 40px 20px;
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
  margin-bottom: 30px;
}

.todo-list {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

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
