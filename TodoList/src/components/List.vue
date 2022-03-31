<template>
  <div>
    <ul class="list">
      <transition-group name="animate__animated animate__bounce" 
        enter-active-class="animate__rubberBand" 
        leave-active-class="animate__backOutRight">
        <item v-for="thing in things" :key="thing.id" :content="thing"></item>
      </transition-group>
    </ul>
  </div>
</template>

<script>
import 'animate.css'
import Item from './Item'
export default {
  components: { Item },
  name: 'List',
  data () {
    return {

    }
  },
  props: ['things']
}
</script>

<style scoped>
/*main*/
.list {
  margin: 0px 50px 10px 50px;
  border-radius: 2px;
  padding: 0px;
  border-radius: 10px;
}
</style>