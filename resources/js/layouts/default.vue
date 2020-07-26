<template>
  <div class="main-layout">
    <navbar />

    <main>
      <search-bar></search-bar>
      <child />
    </main>
  </div>
</template>

<script>
import Navbar from '../components/Navbar'
import Child from '../components/Child'
import SearchBar from './SearchBar'

export default {
  name: 'MainLayout',

  components: {
    SearchBar,
    Child,
    Navbar
  }
}
</script>

<style scoped>
  main {
    position: absolute;
    width: calc(100% - 230px);
    top: 0;
    right: 0;
    height: 100%;
    padding: 0 2.5%;
  }
</style>
