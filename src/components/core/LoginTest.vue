<template>
  <div>
    <el-row>
      <el-form ref="form" :model="editForm" label-width="80px">
        <el-form-item label="账号">
          <el-input v-model="editForm.userNumber"></el-input>
        </el-form-item>
        <el-form-item label="密码">
          <el-input v-model="editForm.userPassword"></el-input>
        </el-form-item>
        <el-button type="primary" @click="login">登录</el-button>
        <el-button type="primary" @click="logout">登出</el-button>
        <el-button type="primary" @click="test1">test1</el-button>
        <el-button type="primary" @click="test2">test2</el-button>
        <el-button type="reset" @click="reset">重置</el-button>
      </el-form>
    </el-row>
  </div>
</template>
<script>

import qs from 'qs'

export default {
  created () {
    this.editForm = Object.assign({}, this.editFormDefault)
    this.token = localStorage.getItem("token")  //以“key”为名称存储一个值“value”
  },
  data () {
    return {
      editFormDefault: {
        userNumber: '13537349601',
        userPassword: ''
      },
      editForm: Object.assign({}, this.editFormDefault)
    }
  },
  methods: {
    login () {
      this.$axiosPost(this.$AiDataApi.core.auth.login,
        this.editForm,
        (response) => {
            let status = 'error'
            if(response.data && response.data.status === 'success'){
                status = 'success'
            }
          this.$message({
            message: response.data.message,
            type: status
          })
        }
      )
    },
    logout(){
      this.$axiosPost(this.$AiDataApi.core.auth.logout,
        this.editForm,
        (response) => {
          this.$message({
            message: response.data.message,
            type: 'success'
          })
        }
      )    
    },
    test1(){
      this.$axiosPost(this.$AiDataApi.core.auth.test1,
        this.editForm,
        (response) => {
          this.$message({
            message: response.data.message,
            type: 'success'
          })
        }
      )    
    },
    test2(){
      this.$axiosPost(this.$AiDataApi.core.auth.test2,
        this.editForm,
        (response) => {
          this.$message({
            message: response.data.message,
            type: 'success'
          })
        }
      )    
    },
    reset () {
      this.editForm = Object.assign({}, this.editFormDefault)
    },

  }
}
</script>