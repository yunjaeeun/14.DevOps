<template>
  <div class="plus">
    <h1>덧셈 기능 만들기</h1>
    <label>num1: </label><input type="text" v-model="num1">&nbsp;
    <label>num2: </label><input type="text" v-model="num2">&nbsp;
    <button @click="sendPlus">더하기</button>
    <hr>
    <p>`{{ num1 }}+{{ num2 }}={{ result }}`</p>
  </div>
</template>

<script setup>
  import {ref} from 'vue';

  const num1 = ref(0);
  const num2 = ref(0);
  const result = ref(0);

  const sendPlus = async() => {
    const response = await fetch(`http://localhost:7777/plus?num1=${num1.value}&num2=${num2.value}`);
    const data = await response.json();
    /*
     sum이라는 프로퍼티 안에 넣어주기 위해서 data.sum으로 선언
     {
      sum:
     }
     */
    result.value = data.sum;      
  }
</script>

<style scoped>
  .plus {
    text-align: center;
  }
</style>
