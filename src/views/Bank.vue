<template>
  <div>
    <h1>Kontojääk:</h1>
    <input v-model.number="konto" placeholder="Sisesta kontonumber">
    <button v-on:click="getBalance()">Kontojääk</button>
    <br>
    {{ balance }}

    <h1>Loo uus konto:</h1>
    <input v-model.number="uuskonto" placeholder="Sisesta konto number">
    <input v-model.number="name" placeholder="Sisesta oma nimi">
    <input v-model.number="newbalance" placeholder="Sisesta algne kontojääk">
    <button v-on:click="newAccount()">Loo konto</button>
    <br>
    {{ staatus }}

    <h1>Raha sissemakse:</h1>
    <input v-model.number="depositAccount" placeholder="Sisesta konto number">
    <input v-model.number="deposit" placeholder="Sisesta sissemakse summa">
    <button v-on:click="updateBalance()">Valmis</button>
    <br>
    {{ staatus2 }}

    <h1>Raha väljamakse:</h1>
    <input v-model.number="withdrawAccount" placeholder="Sisesta konto number">
    <input v-model.number="withdraw" placeholder="Sisesta väljamakse summa">
    <button v-on:click="withdrawMoney()">Valmis</button>
    <br>
    {{ staatus3 }}

    <h1>Tee uus makse:</h1>
    <input v-model.number="fromAccount" placeholder="Sisesta maksja kontonumber">
    <input v-model.number="transfer" placeholder="Sisesta summa">
    <input v-model.number="toAccount" placeholder="Sisesta saaja kontonumber">
    <button v-on:click="transferMoney()">Tee makse</button>
    <br>
    {{ staatus4 }}

    <h1>Konto staatuse muutmine:</h1>
    <input v-model.number="accountnr" placeholder="Sisesta kontonumber">
    <button v-on:click="lock()">Block</button>
    <button v-on:click="unlock()">Unblock</button>
    <br>
    {{ staatus5 }}

  </div>
</template>

<script>

export default {
  data: function () {
    return {
      "konto": '',
      "balance": '',
      "uuskonto": '',
      "name": '',
      "newbalance": '',
      "staatus": '',
      'depositAccount': '',
      'deposit': '',
      'staatus2': '',
      'withdrawAccount': '',
      'withdraw': '',
      'staatus3': '',
      'fromAccount': '',
      'transfer': '',
      'toAccount': '',
      'staatus4': '',
      'accountnr': '',
      'staatus5': ''
    }
  },
  methods: {
    "getBalance": function () {
      this.$http.get('/api/repobank/account/' + this.konto)
          .then(response => {
            console.log(response);
            this.balance = 'Konto jääk on: ' + response.data
          })
          .catch(response => {
            this.balance = response.response.data.message
          })
    },
    "newAccount": function () {
      this.$http.post('/api/repobank/createnewaccount/' + this.uuskonto + '/' + this.name + '/' + this.newbalance)
          .then(response => {
            console.log(response);
            this.staatus = 'Uus konto on loodud' + response.data
          })
          .catch(response => {
            this.staatus = response.response.data.message
          })
    },
    "updateBalance": function () {
      this.$http.put('/api/repobank/deposit/' + this.depositAccount + '/' + this.deposit)
          .then(response => {
            console.log(response);
            this.staatus2 = 'Sissemakse tehtud. Konto jääk: ' + response.data
          })
          .catch(response => {
            this.staatus2 = response.response.data.message
          })
    },
    "withdrawMoney": function () {
      this.$http.put('/api/repobank/withdraw/' + this.withdrawAccount + '/' + this.withdraw)
          .then(response => {
            console.log(response);
            this.staatus3 = 'Väljamakse tehtud. Konto jääk: ' + response.data
          })
          .catch(response => {
            this.staatus3 = response.response.data.message
          })
    },
    "transferMoney": function () {
      this.$http.put('/api/repobank/transfer/' + this.fromAccount + '/' + this.transfer + '/' + this.toAccount)
          .then(response => {
            console.log(response);
            this.staatus4 = response.data
          })
          .catch(response => {
            this.staatus4 = response.response.data.message
          })
    },
    "lock": function () {
      this.$http.put('/api/repobank/account/' + this.accountnr + '/lock')
          .then(response => {
            console.log(response);
            this.staatus5 = response.data
          })
          .catch(response => {
            this.staatus5 = response.response.data.message
          })
    },
    "unlock": function () {
      this.$http.put('/api/repobank/account/' + this.accountnr + '/unlock')
          .then(response => {
            console.log(response);
            this.staatus5 = response.data
          })
          .catch(response => {
            this.staatus5 = response.response.data.message
          })
    }

  }

}

</script>
