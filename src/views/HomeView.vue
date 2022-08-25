<template>
  <div>
    <div v-for="ob in obj">
      <img :src="ob.picture" alt="" />

      <vue-drawing-canvas
        class="drawing-canvas"
        backgroundColor="transparent"
        width="1200"
        height="700"
        lineJoin="round"
        :color="canvasColor"
      />

      <footer class="bottom">
        <div class="answer">
          <div v-if="typeof ob.answer == 'number'" class="answer-number">
            <input type="number" v-model="userAnswer" @submit="checkAnswer" />
            <button class="answer" @click="checkAnswer(ob.answer)">A</button>
          </div>
          <div v-else class="answer-string">
            <button class="answer" @click="checkAnswer(A)">A</button>
            <button class="answer" @click="checkAnswer(B)">B</button>
            <button class="answer" @click="checkAnswer(C)">C</button>
            <button class="answer" @click="checkAnswer(D)">D</button>
            <button class="answer" @click="checkAnswer(E)">E</button>
          </div>
        </div>

        <!-- <input type="number" /> -->
        <button class="next-question" @click="fetchData">NEXT QUESTION</button>

        <div class="colors">
          <button @click="canvasColor = 'black'" class="black"></button>
          <button @click="canvasColor = 'green'" class="green"></button>
          <button @click="canvasColor = 'red'" class="red"></button>
        </div>
      </footer>
    </div>
  </div>
</template>

<script setup>
/*
  IMPORTS
*/

import { onMounted, reactive, ref } from "vue";
import VueDrawingCanvas from "vue-drawing-canvas";

/*
  CONSTANTS
*/

const obj = reactive({});
const userAnswer = ref("");
const canvasColor = ref("black");

onMounted(() => {
  fetchData();
});

const fetchData = () => {
  fetch("/math/data_math.json")
    .then((r) => r.json())
    .then(
      (json) => {
        let randInt = Math.floor(Math.random() * 30) + 1;
        obj.value = json.math.find((element) => element.id == randInt);
      },
      (response) => {
        console.log("Error loading json:", response);
      }
    );
};

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
  width: 75%;
}

.bottom {
  display: flex;
  position: absolute;
  bottom: 0;
  margin-bottom: 1rem;

  z-index: 3;
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

.drawing-canvas {
  border: 1px solid black;
  z-index: 2;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  margin-top: -100px !important;
}

.colors {
  button {
    border-radius: 50%;
  }
  .black {
    background: black;
  }

  .red {
    background: red;
  }

  .green {
    background: green;
  }
}
</style>
