<template>
  <div id="app">
    <router-view/>
    <customer-modal></customer-modal>
  </div>
</template>

<script>
  import CustomerModal from '@/components/CustomerModal'

  export default {
    name: 'app',
    components: {CustomerModal}
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
