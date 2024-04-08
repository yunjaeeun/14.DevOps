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

    /* vue cors 적용 전 */
    // const response = await fetch(`http://localhost:8055/plus?num1=${num1.value}&num2=${num2.value}`);

    /* vue cors 적용 후 */
    // const response = await fetch(`http://localhost:5173/api/plus?num1=${num1.value}&num2=${num2.value}`);

    /* docker containere 간의 네트워크 연결 후 (5173/api가 아니라 8011/api로 바꿔야 한다.)*/
    // const response = await fetch(`http://localhost:8011/api/plus?num1=${num1.value}&num2=${num2.value}`);

    /* 백엔드를 쿠버네티스를 활용한 워커노드로 띄웠을 경우(30001번 NordPort) */
    const response = await fetch(`http://localhost:30001/plus?num1=${num1.value}&num2=${num2.value}`);
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
