<template>
  <div id="app">
    <div class="app-container">
      <header class="app-header">
        <div>
          <p class="eyebrow">MY PRODUCTIVITY</p>
          <h1>To Do List</h1>
          <p class="subtitle">Keep track of what needs to get done.</p>
        </div>
      </header>

      <AddTask @add-task="addTask" />

      <p v-if="tasks.length === 0" class="no-tasks">No tasks available.</p>

      <div v-else class="todo-list">
        <TaskItem
          v-for="task in tasks"
          :key="task.id"
          :task="task"
          @complete="completeTask"
          @delete="deleteTask"
        />
      </div>
    </div>
  </div>
</template>

<script>
import AddTask from './components/AddTask.vue'
import TaskItem from './components/TaskItem.vue'

export default {
  name: 'App',

  components: {
    AddTask,
    TaskItem,
  },

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

  methods: {
    addTask(task) {
      const newTask = {
        id: Date.now(),
        title: task.title,
        completed: false,
        priority: task.priority,
      }

      this.tasks.push(newTask)
    },

    completeTask(taskId) {
      const task = this.tasks.find((task) => task.id === taskId)

      if (task) {
        task.completed = true
      }
    },

    deleteTask(taskId) {
      this.tasks = this.tasks.filter((task) => task.id !== taskId)
    },
  },
}
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #f5f7fb;
  color: #172033;
  font-family:
    Inter,
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    sans-serif;
}

#app {
  min-height: 100vh;
  padding: 60px 20px;
}

.app-container {
  width: 100%;
  max-width: 760px;
  margin: 0 auto;
}

.app-header {
  margin-bottom: 32px;
}

.eyebrow {
  margin: 0 0 8px;
  color: #6366f1;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 1.5px;
}

h1 {
  margin: 0;
  font-size: 42px;
  line-height: 1.1;
  letter-spacing: -1.5px;
}

.subtitle {
  margin: 10px 0 0;
  color: #7a8499;
  font-size: 16px;
}

.todo-list {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.no-tasks {
  padding: 50px 20px;
  text-align: center;
  color: #8a94a6;
  background: white;
  border: 1px solid #e8ebf1;
  border-radius: 16px;
}
</style>
