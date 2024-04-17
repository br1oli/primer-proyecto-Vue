<script setup>
import { ref, computed } from "vue";


const name = "Vue Dinámico";

const counter = ref(0);
const favorites = ref([])

const increment = () => {
    counter.value++;
};

const decrement = () => {
    counter.value--;
};

const reset = () => {
    counter.value = 0;
};

const add = () => {
  favorites.value.push(counter.value)
}

const bloquearBtnAdd = computed(() => {
  const numSearch = favorites.value.find(num => num === counter.value)
  console.log(numSearch)
  if(numSearch === 0) return true;
  return numSearch ? true : false;
})

const classCounter = computed(()=> {
  if(counter.value === 0) {
    return 'zero'
  }
  if(counter.value > 0) {
    return 'positive'
  }
  if(counter.value < 0) {
    return 'negative'
  }
})
</script>

<template>
  <div class="container text-center">
    <div>
      <h1>Hola {{ name }}!</h1>
    </div>
    <h2 :class="classCounter">
        {{ counter }}
    </h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Incremet</button>
      <button @click="decrement" class="btn btn-danger">Decrement</button>
      <button @click="reset" class="btn btn-secondary">Reset</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add favorite</button>
    </div>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num, index) in favorites" :key="index">
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<style>
.negative {
    color: red;
}

.positive {
    color: green;
}

.zero {
  color: peru;
}
</style>