<template>
  <div class="add-task">
    <div class="input-wrapper">
      <input
        v-model="newTaskTitle"
        type="text"
        placeholder="What needs to be done?"
        @keyup.enter="addTask"
      />
    </div>

    <select v-model="newTaskPriority">
      <option value="High">High</option>
      <option value="Medium">Medium</option>
      <option value="Low">Low</option>
    </select>

    <button @click="addTask">
      <span>+</span>
      Add task
    </button>
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

      this.$emit('add-task', {
        title: this.newTaskTitle.trim(),
        priority: this.newTaskPriority,
      })

      this.newTaskTitle = ''
    },
  },
}
</script>

<style scoped>
.add-task {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px;
  margin-bottom: 24px;
  background: white;
  border: 1px solid #e6e9f0;
  border-radius: 16px;
  box-shadow: 0 8px 30px rgba(31, 41, 55, 0.06);
}

.input-wrapper {
  flex: 1;
}

input,
select {
  height: 46px;
  border: 1px solid #e3e7ef;
  border-radius: 10px;
  background: #f8f9fc;
  color: #172033;
  font-size: 14px;
  outline: none;
  transition: 0.2s ease;
}

input {
  width: 100%;
  padding: 0 14px;
}

select {
  padding: 0 12px;
  cursor: pointer;
}

input:focus,
select:focus {
  border-color: #6366f1;
  background: white;
  box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
}

input::placeholder {
  color: #9aa3b2;
}

button {
  height: 46px;
  padding: 0 18px;
  display: flex;
  align-items: center;
  gap: 7px;
  border: none;
  border-radius: 10px;
  background: #6366f1;
  color: white;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: 0.2s ease;
}

button:hover {
  background: #5558e8;
  transform: translateY(-1px);
}

button span {
  font-size: 20px;
  line-height: 1;
}

@media (max-width: 600px) {
  .add-task {
    flex-direction: column;
    align-items: stretch;
  }

  input,
  select,
  button {
    width: 100%;
  }
}
</style>
