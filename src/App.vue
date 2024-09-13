<template>
  <div id="app">
    <main class="layout">
      <div class="top-row">
        <section class="card counter-card">
          <h1>Counter</h1>
          <p>Count: {{ count }}</p>
          <div class="button-container">
            <button @click="decrementCount" aria-label="Decrement Count" class="counter-button">
              &#8722; <!-- Minus sign -->
            </button>
            <button @click="incrementCount" aria-label="Increment Count" class="counter-button">
              &#43; <!-- Plus sign -->
            </button>
          </div>
          <div class="popcat-animation">
            <img :src="popcatImage" alt="Popcat Animation" />
          </div>
        </section>

        <div class="center-text">
          <h2>Vue App by Bren</h2>
        </div>

        <section class="card color-card">
          <h2>Color Box</h2>
          <div :style="{ backgroundColor: boxColor }" class="color-box" aria-label="Color Box"></div>
          <div class="color-picker-container">
            <input type="color" v-model="boxColor" class="color-picker" aria-label="Pick Color"/>
            <button @click="changeColor" aria-label="Change Color">
              Change Color
            </button>
          </div>
        </section>
      </div>

      <section class="card carousel-card">
        <h2>Image Carousel</h2>
        <div class="carousel">
          <img 
            :src="images[currentImage]" 
            :alt="`Carousel image ${currentImage + 1}`" 
            class="carousel-image"
            @error="handleImageError"
            v-if="!imageError"
          />
          <p v-else>Error loading image</p>
          <div class="button-container carousel-buttons">
            <button @click="prevImage" aria-label="Previous Image" class="arrow-button">
              &#9664;
            </button>
            <button @click="nextImage" aria-label="Next Image" class="arrow-button">
              &#9654;
            </button>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      count: 0,
      boxColor: '#e0f7fa',
      images: [
        'https://plus.unsplash.com/premium_photo-1723983556753-1eef0b499e15?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        'https://plus.unsplash.com/premium_photo-1723983556753-1eef0b499e15?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        'https://plus.unsplash.com/premium_photo-1724338542109-0e68d3e7097d?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        'https://plus.unsplash.com/premium_photo-1723983556080-bc59d9b2c5a3?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        'https://plus.unsplash.com/premium_photo-1723983555993-94486b64a509?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        'https://plus.unsplash.com/premium_photo-1723983555331-f2826349f8d8?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        'https://plus.unsplash.com/premium_photo-1723058413328-40a64decb9d3?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        'https://plus.unsplash.com/premium_photo-1722593856461-0adf92daf500?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        'https://images.unsplash.com/photo-1634998794483-1880151ebedf?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        'https://plus.unsplash.com/premium_photo-1690957591806-95a2b81b1075?q=80&w=2071&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
        'https://static.wikia.nocookie.net/herofanon/images/b/ba/A64023B8-2C84-40F3-821F-31B27A6228AC.png'
      ],
      currentImage: 0,
      colors: ['#e0f7fa', '#c8e6c9', '#f8bbd0', '#ffcdd2'],
      imageError: false,
      popcatImage: 'https://popcat.click/twitter-card.jpg', // Default image
      autoChangeInterval: null
    };
  },
  methods: {
    incrementCount() {
      this.count++;
      this.updatePopcatImage();
    },
    decrementCount() {
      if (this.count > 0) this.count--;
      this.updatePopcatImage();
    },
    updatePopcatImage() {
      const images = [
        'https://popcat.click/twitter-card.jpg',
        'https://e0.pxfuel.com/wallpapers/506/346/desktop-wallpaper-popcat-meme-cat.jpg'
      ];
      this.popcatImage = images[this.count % images.length];
    },
    changeColor() {
      const randomIndex = Math.floor(Math.random() * this.colors.length);
      this.boxColor = this.colors[randomIndex];
    },
    nextImage() {
      this.currentImage = (this.currentImage + 1) % this.images.length;
      this.imageError = false;
    },
    prevImage() {
      this.currentImage = (this.currentImage - 1 + this.images.length) % this.images.length;
      this.imageError = false;
    },
    handleImageError() {
      this.imageError = true;
    },
    startAutoChange() {
      this.autoChangeInterval = setInterval(() => {
        this.nextImage();
      }, 5000); // Change image every 5 seconds
    },
    stopAutoChange() {
      clearInterval(this.autoChangeInterval);
    }
  },
  mounted() {
    this.startAutoChange();
  },
  beforeUnmount() {
    this.stopAutoChange();
  }
}
</script>

<style>
:root {
  --color-background: #2c2c2c;
  --color-text: #eaeaea;
  --color-button: #000000;
  --color-button-hover: #4d4e4c;
  --color-border: #444;
  --color-box-shadow: rgba(0, 0, 0, 0.2);
}

html, body {
  height: 100%;
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Roboto', sans-serif;
  text-align: center;
  color: var(--color-text);
  background-color: var(--color-background);
  min-height: 100vh;
  width: 100%;
  margin: 0;
  padding: 20px;
  box-sizing: border-box;
}

.layout {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-width: 1300px;
  margin: 0 auto;
}

.top-row {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

.card {
  background-color: #333;
  border-radius: 12px;
  box-shadow: 0 6px 12px var(--color-box-shadow);
  padding: 20px;
  border: 1px solid var(--color-border);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.7);
}

.counter-card {
  flex: 1;
  min-width: 300px;
  max-width: 400px;
  margin-right: 185px;
}

.color-card {
  flex: 1;
  min-width: 300px;
  max-width: 400px;
  margin-left: 185px;
}


.carousel-card {
  width: 95%;
  max-width: 3000px;
  margin: 0 auto;
}

.color-box {
  width: 100%;
  height: 250px;
  margin: 10px auto 20px;
  border-radius: 12px;
  border: 1px solid var(--color-border);
  transition: background-color 0.50s ease;
}

.color-picker-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin-top: 20px;
}

.color-picker {
  border: none;
  cursor: pointer;
  padding: 0;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  box-shadow: 0 4px 8px var(--color-box-shadow);
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  background-color: transparent;
  overflow: hidden;
}

.color-picker::-webkit-color-swatch-wrapper {
  padding: 0;
}

.color-picker::-webkit-color-swatch {
  border: none;
  border-radius: 50%;
}

.color-picker::-moz-color-swatch {
  border: none;
  border-radius: 50%; /* Memastikan warna tetap berubah di firefox*/
}

.color-picker-container button {
  background-color: var(--color-button);
  color: #ffffff;
  border: none;
  padding: 10px 15px;
  cursor: pointer;
  border-radius: 5px;
  font-size: 16px;
  transition: background-color 0.3s ease;
}

.color-picker-container button:hover {
  background-color: var(--color-button-hover);
}

.carousel {
  margin-top: 20px;
}

.carousel-image {
  max-width: 100%;
  height: auto;
  border-radius: 12px;
}

.button-container {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 10px;
}

.button-container button {
  background-color: var(--color-button);
  color: #fff;
  border: none;
  padding: 10px 15px;
  cursor: pointer;
  border-radius: 5px;
  font-size: 18px;
  transition: background-color 0.3s ease;
}

.button-container button:hover {
  background-color: var(--color-button-hover);
}

.arrow-button {
  font-size: 24px;
  padding: 10px;
}

.counter-button {
  font-size: 24px;
  padding: 10px 15px;
}

.popcat-animation {
  margin-top: 20px;
}

.popcat-animation img {
  max-width: 150px;
  height: auto;
}

.center-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1;
  background-color: rgba(44, 44, 44, 0.8);
  padding: 10px 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.center-text h2 {
  margin: 0;
  font-size: 24px;
  color: #ffffff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.top-row {
  position: relative;
}

@media (max-width: 768px) {
  .center-text {
    position: static;
    transform: none;
    margin: 20px 0;
  }
}

@media (max-width: 768px) {
  .top-row {
    flex-direction: column;
    align-items: center;
  }

  .counter-card, .color-card {
    width: 95%;
    max-width: none;
  }
  
  .color-box {
    height: 150px;
  }

  .popcat-animation img {
    max-width: 120px;
  }
}
</style>