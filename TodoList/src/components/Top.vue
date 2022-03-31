<template>
  <div>
    <input placeholder="请输入代办事项..." @keydown.enter="add" />
  </div>
</template>

<script>
import { nanoid } from 'nanoid'
export default {
  name: 'Top',
  data () {
    return {

    }
  },
  methods: {
    add (event) {
      // 1.获取输入内容
      let content = event.target.value;
      // 2.封装清单事项对象
      let thing = {
        id: nanoid(),
        content: content,
        finish: false
      }
      console.log(thing)
      // 3.存入对象到清单列表
      this.addMethod(thing);
      // 4.清空输入框
      event.target.value = null;
    }
  },
  props: ['addMethod']
}
</script>

<style scoped>
input {
  outline-style: none;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 10px 5px;
  margin: 10px 110px;
  width: 370px;
  font-size: 20px;
  font-family: 'Microsoft soft';
}
input:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(102, 175, 233, 0.6);
}
</style>