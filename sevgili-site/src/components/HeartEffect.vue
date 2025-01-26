<template>
  <div class="heart-container" @mousemove="createHeart">
  </div>
</template>

<script>
export default {
  methods: {
    createHeart(event) {
      const heart = document.createElement("div");
      heart.innerHTML = "❤️";
      heart.classList.add("heart");

      // Kalp pozisyonunu belirle
      heart.style.left = `${event.clientX}px`;
      heart.style.top = `${event.clientY}px`;

      document.body.appendChild(heart);

      // Animasyonu başlat
      setTimeout(() => {
        heart.style.transform = "translateY(-100px) scale(1.5)";
        heart.style.opacity = "0";
      }, 50);

      // 2 saniye sonra kalbi DOM'dan kaldır
      setTimeout(() => {
        heart.remove();
      }, 2000);
    }
  }
};
</script>

<style>
.heart-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 10;
}

.heart {
  position: absolute;
  font-size: 20px;
  transition: all 2s ease-out;
  opacity: 1;
}
</style>
