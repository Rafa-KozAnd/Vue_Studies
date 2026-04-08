<template>
  <div id="app">
    <h1>Planner Semanal</h1>
    <div v-for="(day, index) in daysOfWeek" :key="index">
      <h3>{{ day }}</h3>
      <ul>
        <li v-for="(task, taskIndex) in tasks[index]" :key="taskIndex">
          {{ task }}
        </li>
      </ul>
      <input v-model="newTask[index]" @keyup.enter="addTask(index)" placeholder="Nova tarefa">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      daysOfWeek: ['Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado', 'Domingo'],
      tasks: [[], [], [], [], [], [], []],
      newTask: ['', '', '', '', '', '', '']
    };
  },
  methods: {
    addTask(dayIndex) {
      if (this.newTask[dayIndex].trim() !== '') {
        this.tasks[dayIndex].push(this.newTask[dayIndex].trim());
        this.newTask[dayIndex] = '';
      }
    }
  }
};
</script>

<style scoped>
h3 {
  color: #4CAF50;
}
input {
  margin-top: 10px;
  padding: 5px;
}
</style>
