<template>
  <div id="app">
    <h1>To Do App</h1>

    <AddTask @add-task="addTask" />

    <div class="todo-list">
      <TaskItem v-for="task in tasks" :key="task.id" :task="task" />
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
</style>
