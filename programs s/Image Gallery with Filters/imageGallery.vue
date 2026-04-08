<template>
  <div class="gallery">
    <h2>Galeria de Imagens com Filtros</h2>
    <input type="file" @change="uploadImage" accept="image/*" multiple />
    <div class="filters">
      <label for="filter">Escolha um filtro:</label>
      <select v-model="selectedFilter">
        <option value="none">Nenhum</option>
        <option value="grayscale(100%)">Preto e Branco</option>
        <option value="sepia(100%)">Sépia</option>
        <option value="brightness(1.5)">Mais Brilho</option>
        <option value="contrast(1.5)">Mais Contraste</option>
      </select>
    </div>
    <div class="image-container">
      <img v-for="(image, index) in images" :key="index" :src="image" :style="{ filter: selectedFilter }" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [],
      selectedFilter: "none"
    };
  },
  methods: {
    uploadImage(event) {
      const files = event.target.files;
      for (let file of files) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.images.push(e.target.result);
        };
        reader.readAsDataURL(file);
      }
    }
  }
};
</script>

<style>
.gallery {
  text-align: center;
  padding: 20px;
}
.image-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 10px;
  margin-top: 20px;
}
img {
  width: 200px;
  height: auto;
  border-radius: 10px;
  transition: filter 0.3s;
}
</style>
