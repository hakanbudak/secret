<template>
  <div class="bg" @click="enableAudio">
    <div class="overlay">
      <CountDown />
      <HeartEffect />
      <h1 class="title">Bugün sıradan bir gün değil, senin için özel bir sürpriz saklı! 🎁</h1>
      <p class="date">01.02.2025'de açılacak...</p>
      <p v-show="showMessage" :class="{'message': true, 'show': showMessage}">
        Özel Not :)
        Çok kısa zamanda tarifsiz duyguları yaşattığın için teşekkür ederim .
        Her anın, her bakışın, her gülüşün içimde derin izler bıraktı.
        Seni tanıdığım günden beri hayatım daha renkli, daha anlamlı.
        Bu yüzden kendimi çok şanslı hissediyorum iyi ki varsın.
        Seni çok seviyorum. 💖
      </p>
      <audio ref="audioPlayer" loop>
        <source src="/Candan-Ercetin-Melek.mp3" type="audio/mp3">
      </audio>
    </div>
  </div>
</template>

<script>
import CountDown from "./components/CountDown.vue";
import HeartEffect from "./components/HeartEffect.vue";

export default {
  components: {
    HeartEffect,
  CountDown
  },
  data() {
    return {
      showMessage: false,
      isPlaying: false,
    };
  },
  mounted() {
    // 10 saniye sonra mesajı göster
    setTimeout(() => {
      this.showMessage = true;
    }, 10000);
  },
  methods: {
    enableAudio() {
      const audio = this.$refs.audioPlayer;

      if (!this.isPlaying) {
        audio.play().then(() => {
          console.log("Müzik başladı!");
          this.isPlaying = true;
        }).catch((error) => {
          console.log("Müzik başlatılamadı:", error);
        });
      }
    }
  }
};
</script>

<style scoped>
.bg {
  background: url("../src/assets/background.jpeg") no-repeat center center;
  background-size: cover;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  text-align: center;
  color: white;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
}

.overlay {
  background: rgba(0, 0, 0, 0.6);
  padding: 20px;
  border-radius: 10px;
}

.title {
  font-size: 2em;
  font-weight: bold;
}

.date {
  font-size: 1.5em;
}

.message {
  font-size: 1.8em;
  color: #ffcc00;
  margin-top: 20px;
  text-align: center;
  max-width: 80%;
  opacity: 0;
  transition: opacity 2s ease-in;
  position: absolute;
  top: 80%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: rgba(0, 0, 0, 0.6);
  padding: 20px;
  border-radius: 10px;
  width: 60%;
}

/* Mesaj görünür olduğunda animasyon ekliyoruz */
.message.show {
  opacity: 1;
}

button {
  padding: 10px 20px;
  margin-top: 10px;
  border: none;
  background: #ff4d6d;
  color: white;
  cursor: pointer;
  border-radius: 5px;
  font-size: 1em;
}

button:hover {
  background: #ff1e4b;
}

@media screen and (max-width: 768px) {
  .bg {
    background-position: center center; /* Küçük ekranda ortaya al */
    background-size: contain; /* Resmi tamamen sığdır */
  }
}
</style>
