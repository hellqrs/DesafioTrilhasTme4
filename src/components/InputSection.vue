<template>
  <section class="input-section">
    <input
      type="text"
      v-model="title"
      placeholder="Adicionar nova tarefa..."
    />
    <textarea
      v-model="description"
      placeholder="Adicionar descrição..."
    ></textarea>
    <button @click="handleAddTask">Adicionar</button>
  </section>
</template>

<script>
import { ref } from 'vue';

export default {
  emits: ['add-task'],
  setup(_, { emit }) {
    const title = ref('');
    const description = ref('');

    const handleAddTask = () => {
      if (title.value.trim() && description.value.trim()) {
        emit('add-task', title.value, description.value);
        title.value = '';
        description.value = '';
      }
    };

    return {
      title,
      description,
      handleAddTask,
    };
  },
};
</script>
