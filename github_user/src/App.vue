<template>
  <div id="app">
    <Search></Search>
    <List></List>
  </div>
</template>

<script>
import Search from './components/search.vue'
import List from './components/list.vue'
export default {
  name: 'App',
  components: {
    Search,List
  }
}
</script>

<style>

</style>
