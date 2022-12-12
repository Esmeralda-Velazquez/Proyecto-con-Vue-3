<script setup>
import { ref, computed } from 'vue'
const name = 'vue dinamico';
const stylecolor = "color:red";
const counter = ref(0);
const arrayFavoritos = ref([]);
const handleClick = () => {
  console.log("me diste click");
}

const increment = () => {
  counter.value++;
}
const decrement = () => {
  counter.value--;
}
const reset = () => (counter.value = 0);

const add = () => {
  arrayFavoritos.value.push(counter.value);
}
const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero';
  }
  if (counter.value > 0) {
    return 'positive';
  }
  if (counter.value < 0) {
    return 'negative';
  }
});
const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find(num => num === counter.value);
  if (numSearch === 0) {
    return true;
  }
  return numSearch ? true : false;
});
</script>

<template>
  <div class="container text-center">
    <h1>Hola {{ name }}</h1>
    <br>
    <h2 :style="stylecolor">Este es un contador </h2>
    <br>
    <h2 :class="classCounter"> {{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-danger">Decrementar</button>
      <button @click="reset" class="btn btn-secondary">Reset</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Agregar</button>
    </div>

    <ul class="list-group">
      <li 
      class="list-group mt-4"
      v-for="(num, index) in arrayFavoritos" :key="index">
        {{ num}}
      </li>
    </ul>
  </div>

</template>

<style>
.positive {
  color: green;
}

.negative {
  color: brown;
}

.zero {
  color: blueviolet;
}
</style>
