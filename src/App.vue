<template>
  <div class="modal" v-if="modal_onoff">
    <div class="modal-box">
      <h3>{{ modal_title }}</h3>
      <p>{{ modal_info }}</p>
      <button @click="modal_toggle" class="modal-close-btn">닫기</button>
    </div>
  </div>

  <div class="main">
    <div class="nav">
      <img class="logo" src="./assets/gg.png" alt="ㅠㅠ" />
      <a href="#" v-for="(menu, i) in menus" :key="i"> {{ menu }} </a>
    </div>

    <h2 :style="make_blue">원룸 어플</h2>

    <div class="item" v-for="(product, i) in products" :key="i">
      <img class="room-img" src="./assets/img1.jpg" />
      <h4>
        <a href="#" @click="modal_toggle(i)">{{ product }} 원룸</a>
      </h4>
      <p>월세: {{ prices[i] }}만원</p>
      <button @click="increase_num(i)">추천하기</button>
      <button @click="decrease_num(i)">비추천하기</button>
      <button @click="reset(i)">추천 수 초기화</button>
      <br />
      <span>추천 수: {{ rmd[i] }}</span>
    </div>
  </div>
</template>

<script>
import itemData from "./assets/data.json";

const products = itemData.map((element) => {
  return element["product"];
});
const prices = itemData.map((element) => {
  return element["price"];
});
const infos = itemData.map((element) => {
  return element["place"];
});
const rmd = new Array(itemData.length).fill(0);

export default {
  name: "App",
  data() {
    return {
      menus: ["Home", "Shop", "Contact", "My Page"],
      prices,
      products,
      rmd,
      modal_title: "",
      modal_info: "",
      modal_onoff: false,
      make_blue: "color: blue",
    };
  },
  methods: {
    increase_num(i) {
      this.rmd[i] += 1;
    },
    decrease_num(i) {
      this.rmd[i] -= 1;
    },
    reset(i) {
      this.rmd[i] = 0;
    },
    modal_toggle(i) {
      if (this.modal_onoff) {
        this.modal_onoff = false;
      } else {
        this.modal_title = products[i];
        this.modal_info = infos[i];
        this.modal_onoff = true;
      }
    },
  },
  components: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.main {
  width: 60%;
  margin: auto;
  border-radius: 10px;
  height: 100%;
  background-color: lightcoral;
}
.nav {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  align-content: stretch;
  background-color: lightblue;
  border-radius: 10px;
  height: 80px;
}
.nav a {
  color: red;
  flex-grow: 1;
  text-decoration-line: none;
}
.logo {
  max-width: 100%;
  max-height: 100%;
  border-radius: 10px;
}

.item {
  background-color: lightsalmon;
  height: 130px;
  margin-top: 10px;
  margin-bottom: 10px;
}
.room-img {
  object-fit: contain;
  max-height: 100%;
  float: left;
}

.modal {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
}
.modal-box {
  width: 30%;
  background: white;
  border-radius: 10px;
  margin: auto;
}
.modal-box h3 {
  padding-top: 20px;
}
.modal-box p {
  padding: 20px;
}
.modal-close-btn {
  margin-bottom: 15px;
}
</style>
