<template>
    <div class="login-wrap">
        <el-form class="login-form" label-position="top" label-width="80px" :model="formdata">
            <h2>智慧自习室管理员后台登录</h2>
            <el-form-item label="用户名">
                <el-input v-model="formdata.username"></el-input>
            </el-form-item>
            <el-form-item label="密码">
                <el-input v-model="formdata.password"></el-input>
            </el-form-item>
            <el-button class="login-btn" type="primary" @click.prevent = "handleLogin()">登录</el-button>
        </el-form>
    </div>
</template>

<script>
export default {
  data () {
    return {
      formdata: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    // 登录请求
    handleLogin () {
      this.$http.post('login', this.formdata)
        .then((res) => {
          const {data, meta: {msg, status}} = res.data
          if (status === 200) {
            this.$message.success(msg)
            this.$router.push({name: 'home'})
          } else {
            this.$message.error(msg)
          }
        })
    }
  }
}
</script>

<style>
.login-wrap {
    height: 100%;
    background-color: #324152;
    display: flex;
    justify-content: center;
    align-items: center;
}
.login-wrap .login-form{
    width: 400px;
    background-color: #fff;
    border-radius: 5px;
    padding: 30px;
}
.login-wrap .login-btn{
    width: 100%;
}
</style>
