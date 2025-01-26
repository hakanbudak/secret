<template>
  <div class="countdown">
    <p>Kalan Süre: {{ remainingTime }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      targetDate: new Date("2025-02-01T00:00:00").getTime(),
      remainingTime: "",
    };
  },
  methods: {
    updateCountdown() {
      const now = new Date().getTime();
      const distance = this.targetDate - now;

      if (distance <= 0) {
        this.remainingTime = "Bugün Açıldı! 🎉";
      } else {
        const days = Math.floor(distance / (1000 * 60 * 60 * 24));
        const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
        const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
        const seconds = Math.floor((distance % (1000 * 60)) / 1000);

        this.remainingTime = `${days} Gün ${hours} Saat ${minutes} Dakika ${seconds} Saniye`;
      }
    }
  },
  mounted() {
    this.updateCountdown();
    setInterval(this.updateCountdown, 1000);
  }
};
</script>

<style scoped>
.countdown {
  font-size: 1.5em;
  margin-top: 20px;
  background: rgba(0, 0, 0, 0.5);
  padding: 10px;
  border-radius: 8px;
}
</style>
