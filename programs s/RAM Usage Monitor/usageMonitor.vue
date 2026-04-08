<template>
  <div class="system-monitor">
    <h2>Monitor de Uso de CPU/RAM</h2>
    <p>Uso da CPU: {{ cpuUsage }}%</p>
    <p>Uso da RAM: {{ ramUsage }}%</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cpuUsage: 0,
      ramUsage: 0
    };
  },
  methods: {
    fetchSystemUsage() {
      fetch("/api/system-usage")
        .then(response => response.json())
        .then(data => {
          this.cpuUsage = data.cpu;
          this.ramUsage = data.ram;
        })
        .catch(error => console.error("Erro ao obter dados do sistema:", error));
    }
  },
  mounted() {
    this.fetchSystemUsage();
    setInterval(this.fetchSystemUsage, 5000);
  }
};
</script>

<style>
.system-monitor {
  text-align: center;
  margin-top: 30px;
  padding: 20px;
  background: #f4f4f4;
  border-radius: 10px;
  font-size: 18px;
}
</style>
