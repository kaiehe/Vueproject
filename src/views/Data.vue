<template>
  <div>
    <h1>Kontode nimekiri</h1>

    <table>
      <tr>
        <th>Account number</th>
        <th>Client</th>
        <th>Balance</th>
        <th>Status</th>
      </tr>
      <tr v-for="account in accounts">
        <td>{{ account.accountNumber }}</td>
        <td>{{ account.client }}</td>
        <td>{{ account.balance }}</td>
        <td>{{ account.blocked }}</td>
      </tr>
    </table>

    <h1>Tehingute ajalugu</h1>

    <table>
      <tr>
        <th>Date</th>
        <th>Account number</th>
        <th>Deposit</th>
        <th>Withdraw</th>
        <th>Balance</th>
      </tr>
      <tr v-for="history in history">
        <td>{{ history.date }}</td>
        <td>{{ history.accountNumber }}</td>
        <td>{{ history.deposit }}</td>
        <td>{{ history.withdraw }}</td>
        <td>{{ history.balance }}</td>
      </tr>
    </table>
  </div>
</template>

<script>

export default {
  data: function () {
    return {
      'accounts': '',
      'accountNumber': '',
      'client': '',
      'history': '',
      'date': '',
      'deposit': '',
      'withdraw': '',
      'balance': ''
    }
  },
  methods: {

},
  mounted() {
    this.$http.get('/api/repobank/allaccounts')
    .then(response => this.accounts = response.data)

    this.$http.get('api/repobank/gethistory')
    .then((response => this.history = response.data))
  }
}
</script>
