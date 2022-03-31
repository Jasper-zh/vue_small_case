<template>
  <div>
    <!-- 用户列表 -->
    <el-row v-show="users.length">
        <el-col :span="4" v-for="(user, index) in users" :key="user.login" :offset="index > 0 ? 0 : 0">
            <el-card :body-style="{ padding: '0px' }">
            <a :href="user.html_url" target="_blank">
                <img :src="user.avatar_url" class="image">
            </a>
            <div style="padding: 14px;">
                <span>{{user.login}}</span>
                <div class="bottom clearfix">
                </div>
            </div>
            </el-card>
        </el-col>
    </el-row>
    <!-- 欢迎页面 -->
    <h1 v-show="isWelcome">欢迎使用！</h1>
    <!-- 加载页面 -->
    <h1 v-show="isLoad">正在加载...</h1>
    <!-- 失败页面 -->
    <h1 v-show="errorMsg">{{errorMsg}}</h1>
  </div>
</template>

<script>
export default {
    data(){
        return {
           users:[],
           isWelcome: true,
           isLoad: false,
           errorMsg: '',
        }
    },
    mounted(){
        this.$bus.$on('listView',(obj)=>{
            this.users = obj.users
            this.isWelcome = obj.isWelcome
            this.isLoad = obj.isLoad
            this.errorMsg = obj.errorMsg
        })
        console.log(this.users)
    }
}
</script>

<style>
  .time {
    font-size: 13px;
    color: #999;
  }
  
  .bottom {
    margin-top: 13px;
    line-height: 12px;
  }

  .button {
    padding: 0;
    float: right;
  }

  .image {
    width: 100%;
    display: block;
  }

  .clearfix:before,
  .clearfix:after {
      display: table;
      content: "";
  }
  
  .clearfix:after {
      clear: both
  }
</style>