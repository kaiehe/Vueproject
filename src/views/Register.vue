<template>
<!--  <div class="home">-->
<!--    <img alt="Vue logo" src="../assets/logo.png">-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
<!--  </div>-->
<!--  <div>-->
<!--    <input v-model="email" placeholder="enter your email">-->
<!--    <button v-on:click="register()">Register</button>-->
<!--  </div>-->
  <div>
    <h1>Korrutustabel</h1>
    <input v-model.number="numA">
    <input v-model.number="numB">
    <button v-on:click="multiply()">Multiply</button>
    {{multiplyAnswer}}
  </div>
</template>
<script>

function multiply() {
  for (let i = 1; i < this.numA +1; i++) {
    for (let j = 1; j < this.numB +1; j++) {
      this.multiplyAnswer = (i * j + "");
    }
  }
}

export default {
  data: function ()  {

  }
}

// export default {
//   data: function () {
//     return {
//       'email': ''
//     }
//   },
//   methods: {
//     'register': function (){
//       alert(this.email);
//     }
//   }
// }
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
//
// export default {
//   name: 'Home',
//   components: {
//     HelloWorld
//   }
// }
</script>
