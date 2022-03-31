<template>
  <div class="app">
    <top :addMethod="add"></top>
    <list :things="things"></list>
    <bottom :things="things" @allSel="all" @delF="delFinsh"></bottom>
  </div>
</template>

<script>
import Bottom from './components/Bottom.vue'
import List from './components/List.vue'
import Top from './components/Top.vue'


export default {
  components: { Top, List, Bottom },
  data () {
    return {
      things: JSON.parse(localStorage.getItem('things')) || []
    }
  },
  mounted () {
    this.$bus.$on('ok', this.ok);
    this.$bus.$on('del', this.del);
    this.$bus.$on('edit', this.edit);
  },
  beforeDestroy () {
    this.$bus.$off('ok');
    this.$bus.$off('del');
  },
  methods: {
    add (thing) {
      this.things.unshift(thing);
    },
    ok (id) {
      this.things.forEach((thing) => {
        if (thing.id === id) thing.finish = !thing.finish;
      })
    },
    del (id) {
      this.things = this.things.filter((thing) => {
        return thing.id !== id;
      })
    },
    all (isAll) {
      this.things.forEach(thing => thing.finish = !isAll)
    },
    delFinsh () {
      this.things = this.things.filter(thing => thing.finish === false);
    },
    edit (id, value) {
      this.things.forEach((thing) => {
        if (thing.id === id) {
          thing.content = value;
        }
      })
    }
  },
  watch: {
    things: {
      deep: true,
      handler (value) {
        localStorage.setItem('things', JSON.stringify(value))
      }
    }
  }
}
</script>

<style>
.app {
  width: 600px;
  border: 1px solid black;
  position: absolute;
  left: 50%;
  margin: 50px 0 0 -300px;
  background-color: #333333;
  border-radius: 20px;
}
</style>