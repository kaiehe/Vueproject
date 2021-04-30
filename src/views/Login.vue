<template>
  <div>
    <h1>Loo uus kasutaja</h1>
    <input v-model="kasutajanimi" placeholder="sisesta kasutajanimi">
    <input v-model="password" placeholder="sisesta parool">
    <input v-model="nimi" placeholder="sisesta oma nimi">
    <button v-on:click="newUser()">Loo uus kasutaja</button>
    {{ staatus }}

    <h1>Logi sisse</h1>
    <input v-model="kasutaja" placeholder="sisesta kasutajanimi">
    <input v-model="parool" placeholder="sisesta parool">
    <button v-on:click="logIn()">Logi sisse</button>
    {{ staatus2 }}

    <button v-on:click="logOut()">Logi välja</button>
    {{ staatus3 }}

  </div>
</template>

<script>

//for logout:
// localStorage.removeItem('user-token') //remove token on logout

export default {
  data: function () {
    return {
      'kasutajanimi': '',
      'password': '',
      'nimi': '',
      'staatus': '',
      'kasutaja': '',
      'parool': '',
      'staatus2': '',
      'staatus3': ''
    }
  },
  methods: {
    "newUser": function () {
      this.$http.post('/api/public/newuser', {
        username: this.kasutajanimi,
        password: this.password,
        client: this.nimi
      })
          .then(response => {
            console.log(response);
            this.staatus = "Uus kasutaja on loodud" + response.data;
          })
          .catch(response => {
            this.staatus = response.response.data.message;
          })

    },
    "logIn": function () {
      this.$http.post('/api/public/login', {
        username: this.kasutaja,
        password: this.parool
      })
          .then(response => {
            let token = response.data;
            localStorage.setItem('user-token', token)
            this.$http.defaults.headers.common['Authorization'] = "Bearer " + token
            console.log(response);
            this.staatus2 = response.data;
          })
          .catch(response => {
            this.staatus2 = response.response.data.message;
          })
    },
    "logOut": function () {
      localStorage.removeItem('user-token')
      location.reload(); //tühjenda vormid
      console.log(response);
      this.staatus3 = "Kasutaja on välja logitud" + response.data;
    }
  }

}
</script>
