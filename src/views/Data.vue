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
  </div>
</template>

<script>

export default {
  data: function () {
    return {
      'accounts': '',
      'accountNumber': '',
      'client': ''
    }
  },
  methods: {

},
  mounted() {
    this.$http.get('/api/repobank/accounthistory')
    .then(response => this.accounts = response.data)
  }
}
</script>
