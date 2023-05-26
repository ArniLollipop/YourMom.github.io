<template>
  <section class="section">
    <h1 class="random_h1" v-if="!joke">
      If you want to get random joke please click to the button
    </h1>
    <button class="random__btn" @click="getJoke">Random joke</button>
    <div class="loading" v-if="loader"></div>
    <p class="random_joke">{{ joke }}</p>
  </section>
</template>

<script>
import HomeView from "./views/HomeView.vue";
import axios from "axios";

export default {
  components: { HomeView },
  name: "App",
  data() {
    return {
      joke: "",
      loader: false,
    };
  },
  methods: {
    getJoke() {
      this.loader = true;
      axios
        .get("https://yo-mama.zoom-app.kz/api/joke/get_random_joke/")
        .then((res) => {
          this.joke = res.data.joke;
          this.loader = false;
        })
        .catch((err) => {
          console.log(err);
          this.loader = false;
        });
    },
  },
};
</script>

<style scoped>
.section {
  display: flex;
  flex: 1;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  max-width: 1440px;
  height: 100vh;
  margin: 0 auto;
}
.random__btn {
  cursor: pointer;
  border: none;
  border-radius: 10px;
  background: white;
  padding: 10px 15px;
  font-size: 22px;
  width: fit-content;
  margin: 0 auto;
}

.random_joke {
  color: white;
  font-size: 20px;
  margin-top: 15px;
}

.random_h1 {
  color: white;
  font-size: 20px;
}

.loading {
  width: 80px;
  height: 80px;
  margin-top: 20px;
}

.loading:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #fff;
  border-color: #fff black #fff black;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
