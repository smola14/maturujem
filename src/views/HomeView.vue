<template>
  <div>
    <div v-for="ob in obj">
      <img :src="ob.picture" alt="" />
    </div>
  </div>

  <footer class="bottom">
    <input type="number" v-model="userAnswer" />
    <button class="answer" @click="checkAnswer">A</button>

    <input type="number" />
    <button class="find-question">F</button>

    <input type="range" />
    <span>green black red</span>
  </footer>
</template>

<script setup>
/*
  IMPORTS
*/

import { onMounted, reactive, ref } from "vue";

/*
  CONSTANTS
*/

const obj = reactive({});
const userAnswer = ref("");

onMounted(() => {
  fetch("/math/data_math.json")
    .then((r) => r.json())
    .then(
      (json) => {
        let randInt = Math.floor(Math.random() * 11) + 1;
        obj.value = json.math.find((element) => element.id == randInt);
      },
      (response) => {
        console.log("Error loading json:", response);
      }
    );
});

const checkAnswer = () => {
  if (userAnswer.value == obj.value.answer) {
    alert("spravne");
  } else {
    alert("nespravne");
  }
};
</script>

<style lang="scss" scoped>
img {
  width: 100%;
}

.bottom {
  position: absolute;
  bottom: 0;
  margin-bottom: 1.5rem;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
  text-align: center;
}

input,
button {
  all: unset;
  font-size: inherit;
  padding: 0.5em 0.8rem;
  margin: 0.1em 0.2em;
  /* the following ensures they're all using the same box-model for rendering */
  -moz-box-sizing: content-box; /* or `border-box` */
  -webkit-box-sizing: content-box;
  box-sizing: content-box;
}

input {
  background: rgba(255, 255, 255, 0.5);
  border-radius: 0.5rem;
  border: 1px solid black;
}

button {
  border-radius: 0.3rem;
  background: lightblue;
  border: 1px solid black;
  cursor: pointer;
}
</style>
