<template>
  <div class="bottom" v-show="all">
    <label>
      <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
      <input type="checkbox" :checked="isAll" @change="allSelect" />
    </label>
    <span>
      <span>已完成{{okNum}}</span>
      / 全部{{all}}
    </span>
    <el-button class="btn" type="danger" size="mini" @click="delFinish">清除已完成任务</el-button>
  </div>
</template>

<script>
export default {
  name: 'Bottom',
  props: ['things'],
  computed: {
    all () {
      return this.things.length;
    },
    okNum () {
      /* foreach */
      // let okNum = 0;
      // this.things.forEach(element => {
      //   if (element.finish) okNum++;
      // });
      // return okNum;

      /* reduce */
      // return this.things.reduce((pre, thing) => {
      //   return pre + (thing.finish ? 1 : 0);
      // }, 0);
      return this.things.reduce((pre, thing) => pre + (thing.finish ? 1 : 0), 0);
    },
    isAll () {
      return this.okNum === this.all && this.all > 0;
    }
  },
  methods: {
    allSelect () {
      // 修改全部的事项的完成属性
      // 修改让App自己去做，这边调用
      //this.allSel(this.isAll)
      this.$emit('allSel', this.isAll);
    },
    delFinish () {
      this.$emit('delF')
    }
  },
}
</script>

<style scoped>
/*footer*/
.bottom {
  height: 40px;
  line-height: 40px;
  padding-left: 5px;
  margin: 5px 50px 10px 50px;
  background-color: #999966;
  border-radius: 10px;
  font-size: 15px;
  font-family: 'STHupo';
}

.bottom label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.bottom label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.bottom button {
  float: right;
  margin: 4px 8px 0 0;
  font-size: 15px;
  font-family: 'YouYuan';
}
</style>