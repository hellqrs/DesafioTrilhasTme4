<template>
  <section class="tasks-section">
    <ul>
      <li
        v-for="(task, index) in tasks"
        :key="index"
        :class="{ completed: task.completed }"
      >
        <span><strong>{{ task.title }}</strong></span>
        <span>{{ task.description }}</span>
        <div class="task-actions">
          <button @click="$emit('toggle-complete', index)" class="complete">✔</button>
          <button @click="editTask(index)">✏️</button>
          <button @click="$emit('delete-task', index)">❌</button>
        </div>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  props: ['tasks'],
  methods: {
    editTask(index) {
      const newTitle = prompt('Editar título da tarefa:', this.tasks[index].title);
      const newDescription = prompt('Editar descrição da tarefa:', this.tasks[index].description);
      if (newTitle !== null && newTitle.trim() !== '') {
        this.$emit('edit-task', index, newTitle, newDescription || this.tasks[index].description);
      }
    },
  },
};
</script>
