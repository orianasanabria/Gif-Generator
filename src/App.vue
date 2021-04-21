<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <main class="p-5 col-12 col-md-6 col-lg-6">
          <div class="row">
            <div class="col-12">
              <h1 class="mb-4">Cat Gif Generator</h1>
              <label class="mb-2">Text</label>
              <input class="mb-3 form-control" type="text" v-model="text" />
              <label class="mb-2">Font size</label>
              <input
                class="mb-3 form-control"
                type="number"
                v-model="fontSize"
              />
            </div>
            <div class="col-6">
              <label class="mb-2">Filter</label>
              <select class="mb-3 form-select" v-model="effect">
                <option value="" selected disabled hidden>Select filter</option>
                <option value="blur">Blur</option>
                <option value="mono">Mono</option>
                <option value="sepia">Sepia</option>
                <option value="negative">Negative</option>
                <option value="paint">Paint</option>
                <option value="pixel">Pixel</option>
              </select>
            </div>
            <div class="col-6">
              <label class="mb-2"
                >Font color
                <span :style="'background-color:' + this.fontColor"></span
              ></label>
              <select class="mb-4 form-select" v-model="fontColor">
                <option value="" selected disabled hidden>Select color</option>
                <option value="white">Blanco</option>
                <option value="blue">Azul</option>
                <option value="green">Verde</option>
                <option value="yellow">Amarillo</option>
                <option value="red">Rojo</option>
              </select>
            </div>
            <button class="mt-4 btn btn-danger" @click="getData()">
              Get kitten
            </button>
          </div>
        </main>
        <img class="p-5 col-12 col-md-6 col-lg-6" :src="image" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      text: "Welcome hooman",
      fontSize: "20",
      effect: "",
      fontColor: "",
      image: "",
    };
  },
  methods: {
    async getData() {
      const url = `https://cataas.com/cat/gif/says/${this.text}?filter=${this.effect}&color=${this.fontColor}&size=${this.fontSize}&type=or`;
      this.image = url;
      try {
        const req = await axios(url);
        if (!req) return;
      } catch (error) {
        console.log(error);
      }
    },
  },
  computed: {
    colores() {
      return {
        "btn-primary": this.fontColor.azul,
        "btn-success": this.fontColor.verde,
        "btn-danger": this.fontColor.rojo,
      };
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: "Poppins", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 35px;
}

span {
  height: 12px;
  width: 12px;
  border-radius: 50%;
  margin-left: 5px;
  display: inline-block;
  border: rgb(204, 204, 204) 1px solid;
}
</style>
