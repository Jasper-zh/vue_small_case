<template>
  <li>
    <label>
      <!-- 选框 -->
      <input type="checkbox" :checked="content.finish" @click="ok(content.id)" />
      <!-- 代办标题 -->
      <span v-show="!content.editing">{{content.content}}</span>
      <input
        v-show="content.editing"
        :value="content.content"
        @keyup.enter="$event.target.blur()"
        @blur="confirmName($event,content)"
      />
    </label>
    <!-- 代办删除 -->
    <el-button class="btn" type="danger" @click="del(content.id)" size="mini">删除</el-button>
    <el-button class="btn" type="primary" size="mini" @click="editing(content)">编辑</el-button>
  </li>
</template>

<script>
export default {
  name: 'Item',
  props: ['content'],
  methods: {
    ok (id) {
      // 触发事件总线ok事件
      this.$bus.$emit('ok', id);
    },
    del (id) {
      // 触发事件总线del事件
      // if (confirm('是否要删除该事项？')) {
      //   this.$bus.$emit('del', id);
      // }
      this.$bus.$emit('del', id);
    },
    editing (content) {
      //给它追加是否在编辑状态的属性
      if (Object.prototype.hasOwnProperty.call(content, 'editing')) {
        content.editing = true;
      } else {
        this.$set(content, 'editing', true);
      }
    },
    confirmName (event, content) {
      // 确认显示
      content.editing = false
      // 改数据
      this.$bus.$emit('edit', content.id, event.target.value)
    }
  },
}
</script>

<style scoped>
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  /* border-radius: 10px; */
  font-size: 15px;
  font-family: 'YouYuan';
  background: #999966;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin: 2px 2px 0 0;
  font-size: 15px;
  font-family: 'YouYuan';
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background-color: #ffff99;
}

li:hover button {
  display: block;
}

li input {
  margin-top: 2px;
}
</style>