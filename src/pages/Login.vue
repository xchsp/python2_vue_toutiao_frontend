<template>
    <div class="container">
  <div class="closeBtn">
      <span class="iconfont iconicon-test"></span>
    </div>
    <div class="logo">
      <span class="iconfont iconnew"></span>
    </div>
      <div class="inputName">
      <authInput
        @input="setUserName"
        err_message="请输入正确的手机号"
        placeholder="请输入手机号"
        rule="^[1][3,4,5,7,8][0-9]{9}$"
      ></authInput>
    </div>

    <div class="inputPwd">
      <authInput
        @input="setPassword"
        @keyup="sendLogin"
        err_message="请输入正确的密码"
        placeholder="请输入密码"
        rule="^\d{3,10}$"
        type="password"
      ></authInput>
  </div>
        <div class="btn">
            <authBtn text="登录" @clickxx="sendLogin"></authBtn>
        </div>
    </div>
</template>

<script>
    import authBtn from '@/pages/components/authBtn'
    import authInput from '@/pages/components/authInput'

    export default {
        name: "Login",
       data() {
        return {
          username: '',
          password: ''
        }
      },

        components:{
          authBtn,
          authInput
        },
        methods:{
          setUserName(name) {
          this.username = name
        },
        setPassword(password) {
          this.password = password
        },

        sendLogin(){
          this.$axios({
            url:'/login',
            method: 'POST',
            data:{
              username:this.username,
              password:this.password,
            }
          }).then(res => {
            console.log(res.message)
            console.log(res.data.user)
            console.log(res.data.token)
            localStorage.setItem('token',res.data.token)
            localStorage.setItem('user_id',res.data.user.username)
            this.$toast.success(res.message)
            setTimeout(()=>{
                this.$router.push({name:'homePage'})
            },1000)
          })

          console.log('sendRegister')
          }
        }
    }
</script>

<style lang="less" scoped>
.container {
  padding: 20/@vv;
}
.closeBtn {
  .iconfont {
    font-size: 27/@vv;
  }
}
.logo {
  display: flex;
  justify-content: center;
  .iconfont {
    color: #d81e06;
    font-size: 126/@vv;
  }
}
.btn {
  margin: 50px auto 0;
}
.register {
  margin-top: 20/@vv;
  text-align: center;
}
</style>
