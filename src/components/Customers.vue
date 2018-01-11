<template>
  <div class="customers container">

    <button class="button is-primary"
            type="button"
            @click="getAllCustomers">
      Get Customers
    </button>

    <div class="container" v-for="(customer, index) in addressList">
      <h2 class="title is-3">{{ customerList[index].name }}</h2>
      <table class="table is-fullwidth">
        <tr>
          <th>Country</th>
          <th>Province</th>
          <th>City</th>
          <th>Street</th>
        </tr>
        <tr v-for="address in customer">
          <td>{{ address.country }}</td>
          <td>{{ address.province }}</td>
          <td>{{ address.city }}</td>
          <td>{{ address.street }}</td>
        </tr>
      </table>
      <address-modal :customerId="customerList[index].id"></address-modal>
    </div>

  </div>
</template>

<script>
  import axios from 'axios'
  import AddressModal from '@/components/AddressModal.vue'

  export default {
    components: {AddressModal},
    name: 'Customers',
    component: {AddressModal},
    data () {
      return {
        customerList: [],
        addressList: []
      }
    },
    methods: {
      getAllCustomers: function () {
        const URL = '/api/customers'

        axios.get(URL)
          .then(response => {
            console.log(response)
            this.customerList = response.data
            this.loadAddress()
          })
          .catch(error => {
            console.log(error)
          })
      },
      loadAddress: function () {
        this.customerList.forEach(customer => {
          let url = '/api/customers/' + customer.id + '/address'
          axios.get(url)
            .then(response => {
              console.log(response.data)
              this.addressList.push(response.data)
            })
            .catch(error => {
              console.log(error)
            })
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  ul {
    list-style-type: none;
  }

  button {
    margin-bottom: 15px;
    margin-top: 15px;
  }

</style>
