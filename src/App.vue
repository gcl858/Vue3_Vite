<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
//import { computed, defineComponent } from "@vue/runtime-core";
import axios from "axios";
import { JsonViewer } from "vue3-json-viewer";
import "vue3-json-viewer/dist/index.css";
import { reactive, ref } from "vue";
let obj = {
  name: "qiu", //字符串
  age: 18, //数组
  isMan: false, //布尔值
  date: new Date(),
  fn: () => {},
  arr: [1, 2, 5],
};
//const jsonData = reactive(obj);

//axios
//接收伺服器的回傳資料
axios.defaults.headers.common["Access-Control-Allow-Origin"] = "*";
const resData = ref();

const getAxios = function () {
  axios
    .get("/api/try/ajax/json_demo.json")
    .then((res) => {
      //獲取伺服器的回傳資料
      resData.value = res.data;
      jsonData.value = res.data;
      console.log(res.data);
    })
    .catch((error) => {
      console.log(error, "失敗");
    });
};
//執行Axios
getAxios();

const jsonData = ref();

const mytest = "append using const message";
</script>

<template>
  <header>
    <div class="wrapper">
      <div>{{ mytest }}</div>
      <div class="box">
        <h2>light</h2>
        <JsonViewer :value="jsonData" copyable boxed sort theme="jv-light" />
      </div>
      <div>
        <h2>我是Axios</h2>
        <div>{{ resData }}</div>
      </div>

      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Ho23dd4me</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>
</template>

<style scoped>
.box {
  margin-top: 1rem;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
