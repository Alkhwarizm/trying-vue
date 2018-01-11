<template>
  <div class="container">

    <button class="button is-small is-link"
            type="button" @click="activateModal">Add Address</button>


    <div class="modal" :class="{ 'is-active': active }">
      <div class="modal-background"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">
            New Address
          </p>
          <button class="delete" aria-label="close" @click="deactivateModal"></button>
        </header>
        <section class="modal-card-body">
          <p>
            #ID: {{ customerId }}
          </p>
          <form>
            <h2 class="title is-3">Address</h2>
            <div class="control">
              <label for="country">Country</label>
              <input id="country" class="input" type="text" v-model="newAddress.country">
            </div>
            <div class="control">
              <label for="province">Province</label>
              <input id="province" class="input" type="text" v-model="newAddress.province">
            </div>
            <div class="control">
              <label for="city">City</label>
              <input id="city" class="input" type="text" v-model="newAddress.city">
            </div>
            <div class="control">
              <label for="street">Street</label>
              <input id="street" class="input" type="text" v-model="newAddress.street">
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
    name: 'AddressModal',
    data () {
      return {
        active: false,
        addressTemplate: {
          country: '',
          province: '',
          city: '',
          street: ''
        },
        newAddress: {
          country: '',
          province: '',
          city: '',
          street: ''
        }
      }
    },
    props: ['customerId'],
    methods: {
      activateModal: function () {
        this.active = true
      },
      deactivateModal: function () {
        this.active = false
      },
      submitNewAddress: function () {
        const url = '/api/customers/' + this.customerId + '/address'
        axios.post(url, this.newAddress)
          .then(response => {
            console.log(response)
            alert('Successfully created new address')
            this.newAddress = this.addressTemplate
            this.deactivateModal()
          })
          .catch(error => {
            console.log(error)
          })
      }
    }
  }
</script>

<style scoped>

</style>
