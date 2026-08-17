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

      <!-- Filters -->
      <div class="filters">
        <div class="filter-group">
          <span class="filter-label">Status</span>

          <button :class="{ active: statusFilter === 'All' }" @click="statusFilter = 'All'">
            All
          </button>

          <button :class="{ active: statusFilter === 'Active' }" @click="statusFilter = 'Active'">
            Active
          </button>

          <button
            :class="{ active: statusFilter === 'Completed' }"
            @click="statusFilter = 'Completed'"
          >
            Completed
          </button>
        </div>

        <div class="filter-group">
          <span class="filter-label">Priority</span>

          <select v-model="priorityFilter">
            <option value="All">All priorities</option>
            <option value="High">High</option>
            <option value="Medium">Medium</option>
            <option value="Low">Low</option>
          </select>
        </div>
      </div>

      <!-- Task list -->
      <p v-if="filteredTasks.length === 0" class="no-tasks">No tasks available.</p>

      <div v-else class="todo-list">
        <TaskItem
          v-for="task in filteredTasks"
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

      statusFilter: 'All',
      priorityFilter: 'All',
    }
  },

  computed: {
    filteredTasks() {
      return this.tasks.filter((task) => {
        const matchesStatus =
          this.statusFilter === 'All' ||
          (this.statusFilter === 'Active' && !task.completed) ||
          (this.statusFilter === 'Completed' && task.completed)

        const matchesPriority =
          this.priorityFilter === 'All' || task.priority === this.priorityFilter

        return matchesStatus && matchesPriority
      })
    },
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

/* Filters */

.filters {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 20px;
  padding: 10px 12px;
  background: white;
  border: 1px solid #e8ebf1;
  border-radius: 14px;
  box-shadow: 0 5px 20px rgba(31, 41, 55, 0.04);
}

.filter-group {
  display: flex;
  align-items: center;
  gap: 6px;
}

.filter-label {
  margin-right: 6px;
  color: #8a94a6;
  font-size: 12px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.filter-group button {
  padding: 8px 12px;
  border: none;
  border-radius: 8px;
  background: transparent;
  color: #737d90;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  transition: 0.2s ease;
}

.filter-group button:hover {
  background: #f3f4f8;
  color: #172033;
}

.filter-group button.active {
  background: #6366f1;
  color: white;
}

.filter-group select {
  padding: 8px 10px;
  border: 1px solid #e3e7ef;
  border-radius: 8px;
  background: #f8f9fc;
  color: #4b5563;
  font-size: 13px;
  outline: none;
  cursor: pointer;
}

.filter-group select:focus {
  border-color: #6366f1;
}

/* Tasks */

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

@media (max-width: 650px) {
  .filters {
    flex-direction: column;
    align-items: stretch;
  }

  .filter-group {
    justify-content: center;
    flex-wrap: wrap;
  }
}
</style>
