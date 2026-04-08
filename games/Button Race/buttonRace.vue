<template>
  <div id="app">
    <h1>Corrida de Botões</h1>
    
    <div class="track">
      <div 
        v-for="(button, index) in buttons" 
        :key="index" 
        class="button" 
        :style="{ left: button.position + 'px' }"
        @click="startRace(index)"
      >
        <span>{{ button.name }}</span>
      </div>
    </div>

    <div v-if="winner" class="winner">
      <h2>O vencedor foi: {{ winner }}</h2>
    </div>
    
    <button @click="resetRace">Reiniciar Corrida</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      buttons: [
        { name: 'Botão 1', position: 0, running: false },
        { name: 'Botão 2', position: 0, running: false },
        { name: 'Botão 3', position: 0, running: false }
      ],
      winner: null,
      raceInterval: null
    };
  },
  methods: {
    startRace(index) {
      if (this.winner) return; // Evita que a corrida comece se já houver um vencedor
      
      if (!this.buttons[index].running) {
        this.buttons[index].running = true;
        this.raceInterval = setInterval(() => {
          this.buttons[index].position += Math.random() * 10; // A cada intervalo, o botão se move
          if (this.buttons[index].position >= 400) {
            clearInterval(this.raceInterval);
            this.winner = this.buttons[index].name;
          }
        }, 50); // Intervalo de movimento do botão
      }
    },
    resetRace() {
      this.buttons.forEach(button => {
        button.position = 0;
        button.running = false;
      });
      this.winner = null;
    }
  }
};
</script>

<style scoped>
.track {
  width: 500px;
  height: 50px;
  background-color: #f3f3f3;
  position: relative;
  margin: 20px 0;
}

.button {
  position: absolute;
  top: 5px;
  width: 100px;
  height: 40px;
  background-color: #4CAF50;
  color: white;
  text-align: center;
  line-height: 40px;
  cursor: pointer;
}

.winner {
  font-size: 20px;
  color: green;
}

button {
  padding: 10px;
  background-color: #2196F3;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #1976D2;
}
</style>
