<template>
  <div class="wrap">
    <el-form class="form" label-position="top" label-width="80px" :model="formData">
      <h2>用户登录</h2>
      <el-form-item label="用户名">
        <el-input v-model="formData.username"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input v-model="formData.password"></el-input>
      </el-form-item>
      <el-button @click="handleLogin()" type="primary" class="btn">登录</el-button>
    </el-form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      formData: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    async handleLogin () {
      const res = await this.$http.post('login', this.formData)
      const {
        data: {
          meta: { msg, status },
          data
        }
      } = res
      if (status === 200) {
        localStorage.setItem('token', data.token)
        this.$router.push({
          name: 'home'
        })
      } else {
        this.$message.warning(msg)
      }
    }
  }
}
</script>

<style>
.wrap {
  height: 100%;
  background-color: #324152;
  display: flex;
  justify-content: center;
  align-items: center;
}

.wrap .form {
  background-color: #fff;
  border-radius: 10px;
  width: 400px;
  padding: 30px;
}
.wrap .form .btn {
  width: 100%;
}
</style>
