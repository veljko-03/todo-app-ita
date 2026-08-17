<template>
  <div class="add-task">
    <input v-model="newTaskTitle" type="text" placeholder="Enter a new task" />

    <select v-model="newTaskPriority">
      <option value="High">High</option>
      <option value="Medium">Medium</option>
      <option value="Low">Low</option>
    </select>

    <button @click="addTask">Add task</button>
  </div>
</template>

<script>
export default {
  name: 'AddTask',

  data() {
    return {
      newTaskTitle: '',
      newTaskPriority: 'Medium',
    }
  },

  methods: {
    addTask() {
      if (this.newTaskTitle.trim() === '') {
        return
      }

      const newTask = {
        title: this.newTaskTitle,
        priority: this.newTaskPriority,
      }

      this.$emit('add-task', newTask)

      this.newTaskTitle = ''
    },
  },
}
</script>

<style scoped>
.add-task {
  display: flex;
  gap: 10px;
  margin-bottom: 30px;
}

input,
select {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}

input {
  flex: 1;
}

button {
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background-color: #42b983;
  color: white;
}

button:hover {
  opacity: 0.85;
}
</style>
