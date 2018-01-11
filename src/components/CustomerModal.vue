<template>
  <div class="container">

    <button class="button is-primary"
            type="button" @click="activateModal">New Customer</button>

    <div class="modal" :class="{ 'is-active': active }">
      <div class="modal-background"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">New Customer</p>
          <button class="delete" aria-label="close" @click="deactivateModal"></button>
        </header>
        <section class="modal-card-body">
          <form>
            <h2>Customer</h2>
            <div class="control">
              <label for="name">Name</label>
              <input id="name" class="input" type="text" v-model="newCustomer.name">
            </div>
            <h2>Address</h2>
            <div class="control">
              <label for="country">Country</label>
              <input id="country" class="input" type="text" v-model="newCustomer.address.country">
            </div>
            <div class="control">
              <label for="province">Province</label>
              <input id="province" class="input" type="text" v-model="newCustomer.address.province">
            </div>
            <div class="control">
              <label for="city">City</label>
              <input id="city" class="input" type="text" v-model="newCustomer.address.city">
            </div>
            <div class="control">
              <label for="street">Street</label>
              <input id="street" class="input" type="text" v-model="newCustomer.address.street">
            </div>

          </form>
        </section>
        <footer class="modal-card-foot">
          <button class="button is-success" @click="submitNewAddress">Submit</button>
          <button class="button" @click="deactivateModal">Cancel</button>
        </footer>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'CustomerModal',
    data () {
      return {
        active: false,
        customerTemplate: {
          name: '',
          address: {
            country: '',
            province: '',
            city: '',
            street: ''
          }
        },
        newCustomer: {
          name: '',
          address: {
            country: '',
            province: '',
            city: '',
            street: ''
          }
        }
      }
    },
    methods: {
      activateModal: function () {
        this.active = true
      },
      deactivateModal: function () {
        this.active = false
      },
      submitNewAddress: function () {
        const url = '/api/customers'
        axios.post(url, this.newCustomer)
          .then(response => {
            console.log(response)
            alert('Sucessfully created new Customer')
            this.newCustomer = this.customerTemplate
          })
          .catch(error => {
            console.log(error)
          })
      }
    }
  }
</script>

<style scoped>
  button {
    margin-bottom: 15px;
    margin-top: 15px;
  }
</style>
