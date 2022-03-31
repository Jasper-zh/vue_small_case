<template>
  <div class="search">
      <h3>Search Github Users</h3>
      <el-input placeholder="请输入内容" class="ipt" v-model="username"></el-input>
      <el-button type="primary" class="btn" size="small"  @click="search">search</el-button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return {
            username: ""
        }
    },
    // https://api.github.com/search/users?q=xxx
    methods:{
        search(){
            //发生请求之前的状态
            this.$bus.$emit('listView',{users:[],isWelcome:false,isLoad:true,errorMsg:''})
            axios.get('https://api.github.com/search/users?q='+this.username).then(
                response=>{
                    // 发送请求成功后
                    this.$bus.$emit('listView',response.data)
                    this.$bus.$emit('listView',{users:response.data.items,isWelcome:false,isLoad:false,errorMsg:''})
                },
                error=>{
                    this.$bus.$emit('listView',{users:[],isLoad:false,errorMsg:error.errorMsg})
                }
            )
        }
    }
}
</script>

<style>
.ipt{
    width: 200px !important;
    margin-right: 10px;
}
.search{
    width: 100%;
    height: 100%;
    background-color: #CCCCCC;
    padding: 15px 0 10px 50px;
    margin-bottom: 10px;
    box-sizing:border-box;
}
</style>