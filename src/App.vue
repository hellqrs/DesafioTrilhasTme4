<template>
  <div id="app">
    <Header />
    <InputSection @add-task="addTask" />
    <TasksSection
      :tasks="tasks"
      @toggle-complete="toggleComplete"
      @edit-task="editTask"
      @delete-task="deleteTask"
    />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import Header from './components/Header.vue';
import InputSection from './components/InputSection.vue';
import TasksSection from './components/TasksSection.vue';

export default {
  components: {
    Header,
    InputSection,
    TasksSection,
  },
  setup() {
    const tasks = ref([]);

    onMounted(() => {
      const savedTasks = JSON.parse(localStorage.getItem('tasks') || '[]');
      tasks.value = savedTasks;
    });

    const saveTasks = (newTasks) => {
      tasks.value = newTasks;
      localStorage.setItem('tasks', JSON.stringify(newTasks));
    };

    const addTask = (title, description) => {
      const newTasks = [...tasks.value, { title, description, completed: false }];
      saveTasks(newTasks);
    };

    const toggleComplete = (index) => {
      const newTasks = tasks.value.map((task, i) => i === index ? { ...task, completed: !task.completed } : task);
      saveTasks(newTasks);
    };

    const editTask = (index, title, description) => {
      const newTasks = tasks.value.map((task, i) => i === index ? { ...task, title, description } : task);
      saveTasks(newTasks);
    };

    const deleteTask = (index) => {
      const newTasks = tasks.value.filter((_, i) => i !== index);
      saveTasks(newTasks);
    };

    return {
      tasks,
      addTask,
      toggleComplete,
      editTask,
      deleteTask,
    };
  },
};
</script>

<style src="./styles.css"></style>
